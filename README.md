# focus-gate-content

Content repository for [Focus Gate](https://github.com/chatura-c/focus-gate), a private Android
app that gates social media apps behind short system-design lessons and quizzes. This repo holds
only the content: a `manifest.json` index, one JSON file per topic under `topics/`, and the schema
that defines their shape — no app code lives here.

See [`SCHEMA.md`](SCHEMA.md) (backed by [`schema/topic.schema.json`](schema/topic.schema.json))
for the full format of a topic file and each question type, and [`CURRICULUM.md`](CURRICULUM.md)
for the running log of what's been covered and what's next.

This repo is public, and is fetched read-only over plain HTTPS
(`raw.githubusercontent.com/chatura-c/focus-gate-content/main/...`) by the Focus Gate Android app
— no auth, no API, no server code. A new `topics/<id>.json` is added most days by an automated job
that picks the next uncovered concept, writes a lesson and mixed-type question set, validates it
against the schema, and commits/pushes here directly. It's also fine to hand-edit or hand-add
topics at any time; the automation just reads `CURRICULUM.md` and `manifest.json` to figure out
what's already covered before it runs.
