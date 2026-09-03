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
| 7 | 2026-08-21 | Database Sharding        | `2026-08-21-database-sharding`      |
| 8 | 2026-08-21 | CDNs                      | `2026-08-21-cdns`                   |
| 9 | 2026-08-26 | Message Queues            | `2026-08-26-message-queues`         |
| 10 | 2026-08-26 | Database Indexing        | `2026-08-26-database-indexing`      |
| 11 | 2026-08-27 | Eventual Consistency      | `2026-08-27-eventual-consistency`   |
| 12 | 2026-08-27 | Circuit Breakers          | `2026-08-27-circuit-breakers`       |
| 13 | 2026-08-28 | Idempotency               | `2026-08-28-idempotency`            |
| 14 | 2026-08-28 | API Gateways              | `2026-08-28-api-gateways`           |
| 15 | 2026-08-29 | Backpressure              | `2026-08-29-backpressure`           |
| 16 | 2026-08-29 | Service Discovery         | `2026-08-29-service-discovery`      |
| 17 | 2026-08-30 | Sagas (Distributed Transactions) | `2026-08-30-sagas`           |
| 18 | 2026-08-30 | Leader Election           | `2026-08-30-leader-election`        |
| 19 | 2026-08-31 | Two-Phase Commit (2PC)    | `2026-08-31-two-phase-commit`       |
| 20 | 2026-08-31 | Bloom Filters             | `2026-08-31-bloom-filters`          |
| 21 | 2026-09-01 | Write-Ahead Logging (WAL) | `2026-09-01-write-ahead-logging`    |
| 22 | 2026-09-03 | Distributed Locking       | `2026-09-03-distributed-locking`    |
| 23 | 2026-09-03 | Vector Clocks / Logical Clocks | `2026-09-03-vector-clocks`     |
| 24 | 2026-09-04 | Quorum Reads and Writes  | `2026-09-04-quorum-consensus`       |
| 25 | 2026-09-04 | gRPC vs REST             | `2026-09-04-grpc-vs-rest`           |
| 26 | 2026-09-05 | Consensus with Raft      | `2026-09-05-consensus-raft`         |
| 27 | 2026-09-05 | Gossip and Anti-Entropy Protocols | `2026-09-05-gossip-protocols` |
| 28 | 2026-09-06 | Session Guarantees (Read-Your-Writes & Monotonic Reads) | `2026-09-06-session-guarantees` |
| 29 | 2026-09-06 | Change Data Capture (CDC) and the Outbox Pattern | `2026-09-06-cdc-outbox` |
| 30 | 2026-09-07 | Sharding Key Design       | `2026-09-07-sharding-key-design`    |
| 31 | 2026-09-07 | LSM-Trees vs B-Trees     | `2026-09-07-lsm-vs-btree`           |
| 32 | 2026-09-08 | Merkle Trees for Replica Reconciliation | `2026-09-08-merkle-trees` |
| 33 | 2026-09-08 | Cache Eviction Policies: LRU, LFU, and TTL | `2026-09-08-cache-eviction-policies` |

## Repetitions (spaced re-quizzes, not new concepts)

| Date       | Concept re-quizzed | New file                            | Notes |
|------------|--------------------|-------------------------------------|-------|
| 2026-09-02 | CAP Theorem (orig. `2026-08-21-cap-theorem`) | `2026-09-02-cap-theorem-review` | Same lesson text, fresh questions covering the CAP definition of availability, AP reconciliation, PACELC, and per-request quorum tuning. |

Note: 2026-08-22 through 2026-08-25 were already filled by hand-seeded content (see `README.md`),
so this run's topics were scheduled for 2026-08-26, the next open date, rather than colliding with
an existing `date` already present in `manifest.json`. Same reasoning applies to 2026-08-27 through
2026-09-05 above — each was the next open date as of its respective run (this keeps a stable
~4-5 day gap between a run's real calendar date and the `date` it assigns, rather than the gap
growing further). The 2026-09-05 topics were generated on the 2026-08-31 run, the 2026-09-06
topics were generated on the 2026-09-01 run, the 2026-09-07 topics were generated on
the 2026-09-02 run, and the 2026-09-08 topics above were generated on the 2026-09-03 run.

## Candidate next topics

Not yet covered — the generation job should pick from here (or an equally well-established
system-design concept not listed) before repeating anything above:

- Multi-Paxos / EPaxos as a contrast to Raft (now that Raft is covered, #26)
- Dead letter queues and poison-message handling (follow-up to Message Queues, #9)
- Read repair vs. hinted handoff as anti-entropy mechanisms (follow-up to Merkle Trees, #32)
- Bulkheads and resource isolation (companion to Circuit Breakers, #12)

## How to append

After publishing a new `topics/<id>.json` and updating `manifest.json`, add a new row to the
"Covered" table above (next `#`, its date, title, and id). If the day's topic was a
spaced-repetition re-quiz of an existing concept rather than a new one, note that in this file
instead of adding a duplicate row for the same underlying concept.
