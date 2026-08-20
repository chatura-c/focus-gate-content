# Curriculum log

Running log of topics covered, in order. The daily generation job should read this (and
`manifest.json`) before picking a new topic, append a new entry here after publishing, and
occasionally schedule a spaced-repetition re-quiz of an older topic instead of only ever adding
new ones.

Seeded by hand on 2026-08-20 (see `README.md` — seed content, not generated).

## Covered

| # | Date       | Topic                  | id                                 |
|---|------------|-------------------------|-------------------------------------|
| 1 | 2026-08-21 | CAP Theorem              | `2026-08-21-cap-theorem`            |
| 2 | 2026-08-22 | Load Balancing           | `2026-08-22-load-balancing`         |
| 3 | 2026-08-23 | Caching Strategies       | `2026-08-23-caching-strategies`     |
| 4 | 2026-08-24 | Database Replication     | `2026-08-24-database-replication`   |
| 5 | 2026-08-25 | Rate Limiting            | `2026-08-25-rate-limiting`          |
| 6 | 2026-08-20 | Consistent Hashing       | `2026-08-20-consistent-hashing`     |

## Candidate next topics

Not yet covered — the generation job should pick from here (or an equally well-established
system-design concept not listed) before repeating anything above:

- Message queues (pub/sub, at-least-once vs exactly-once delivery)
- Database sharding / partitioning
- CDNs
- Database indexing (B-trees, when an index helps vs. hurts)
- Eventual consistency
- Circuit breakers
- Idempotency (idempotency keys, safe retries)
- API gateways
- Backpressure

## How to append

After publishing a new `topics/<id>.json` and updating `manifest.json`, add a new row to the
"Covered" table above (next `#`, its date, title, and id). If the day's topic was a
spaced-repetition re-quiz of an existing concept rather than a new one, note that in this file
instead of adding a duplicate row for the same underlying concept.
