# Content schema

Source of truth: [`schema/topic.schema.json`](schema/topic.schema.json) (JSON Schema, draft 2020-12).
This document is a human-readable companion — if the two ever disagree, the schema file wins.

Every file under [`topics/`](topics/) is one JSON object that must validate against that schema.
[`manifest.json`](manifest.json) is a flat index of all topic files (not itself covered by this schema).

## Top-level topic object

| Field      | Type   | Notes |
|------------|--------|-------|
| `id`       | string | `YYYY-MM-DD-slug`, must match the filename (`topics/<id>.json`) and `date`. |
| `date`     | string | ISO date `YYYY-MM-DD` the topic is scheduled for. |
| `title`    | string | Human-readable title, e.g. `"CAP Theorem"`. |
| `category` | string | Currently always `"system-design"`. |
| `lesson`   | string | Plain text / markdown, a few paragraphs, teachable standalone (read before any quiz). |
| `questions`| array  | One or more question objects (see below). Seed topics include at least one of each type. |

## Question objects

Every question has these common fields, plus type-specific ones. `type` determines which shape
applies (`oneOf` in the schema — a question must match exactly one branch).

Common to all types:

| Field         | Type   | Notes |
|---------------|--------|-------|
| `id`          | string | Unique within the topic, e.g. `"q1"`. |
| `type`        | string | One of `mcq`, `true_false`, `fill_blank`, `ordering`. |
| `prompt`      | string | The question text. |
| `explanation` | string | One sentence explaining why the answer is correct, shown after answering. |

### `mcq`

Adds `options` (array of choice strings, presented in order) and `answer` (zero-based index into
`options` giving the correct choice).

```json
{
  "id": "q1",
  "type": "mcq",
  "prompt": "Under a network partition, a CP system will:",
  "options": [
    "Continue serving reads and writes on every node",
    "Reject requests on the minority side to preserve consistency",
    "Always favor availability over consistency",
    "Shut down entirely until the partition heals"
  ],
  "answer": 1,
  "explanation": "CP systems sacrifice availability on the minority side of a partition so every acknowledged read/write stays consistent."
}
```

### `true_false`

Adds `answer` (boolean — whether `prompt` is a true statement).

```json
{
  "id": "q2",
  "type": "true_false",
  "prompt": "CAP theorem says a distributed system can only ever provide two of consistency, availability, and partition tolerance, at all times, in every configuration.",
  "answer": false,
  "explanation": "Partition tolerance isn't optional for a distributed system, so the real tradeoff during a partition is consistency vs. availability, not a free pick of any two."
}
```

### `fill_blank`

Adds `answer` (the canonical correct string, matched case-insensitively by the app) and optional
`acceptable` (array of additional strings also accepted).

```json
{
  "id": "q3",
  "type": "fill_blank",
  "prompt": "A CP system that requires a majority of replicas to agree before acknowledging a write is using a ____.",
  "answer": "quorum",
  "acceptable": ["quorum write", "majority quorum"],
  "explanation": "Requiring a majority (quorum) of replicas to agree is how CP systems keep reads and writes consistent despite node failures."
}
```

### `ordering`

Adds `items` (array of strings in the order presented to the user — should be shuffled, not
pre-sorted) and `answer` (array of zero-based indices into `items` giving the correct order; same
length as `items`, each index used exactly once).

```json
{
  "id": "q4",
  "type": "ordering",
  "prompt": "Order these steps of a leader-follower failover, earliest first.",
  "items": [
    "A new leader is elected from the remaining followers",
    "Followers stop receiving heartbeats from the leader",
    "Clients are redirected to the new leader",
    "The leader crashes or becomes unreachable"
  ],
  "answer": [3, 1, 0, 2],
  "explanation": "Failover starts with the leader going down, is detected via missed heartbeats, resolved by electing a new leader, then clients are pointed at it."
}
```

## Validating

```bash
# Node + ajv
npx ajv-cli validate -s schema/topic.schema.json -d "topics/*.json" --spec=draft2020

# Python + jsonschema
python3 -c "
import json, glob, jsonschema
schema = json.load(open('schema/topic.schema.json'))
for f in glob.glob('topics/*.json'):
    jsonschema.validate(json.load(open(f)), schema)
    print(f, 'OK')
"
```
