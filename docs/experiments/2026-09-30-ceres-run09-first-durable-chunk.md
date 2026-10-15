> Imported from [DeepFin at 32370b099f6d](https://github.com/jjoshua2/DeepFin/blob/32370b099f6d8d4ec965de135e70a752fc95a7a9/docs/experiments/2026-09-30-ceres-run09-first-durable-chunk.md). [Original bytes](https://github.com/jjoshua2/DeepFin-research/blob/8536ec99471478efee257e9b7bbeb4d3e614854b/docs/experiments/2026-09-30-ceres-run09-first-durable-chunk.md) and source history remain available. Historical commands and local artifact paths describe their original run.

# Ceres source run09: first durable chunk

**Zero corpus, label, pack, and training admission.**

Run09 resumed after the 51 completed run08 chunks (indices 0–50) were rechecked and fsynced under a quiet, bounded prefix seal. The source still uses 1,024 games per chunk and one active fixed32 GPU worker. The first new chunk, index 51, completed 1,024 games with no discards. Its game IDs begin at 62,464, exactly 1,024 after chunk 50's start.

Chunk 51 produced 127,792 gross accepted feed rows and 125,489 unique feeds; the cumulative unique source count is 6,589,934. The physical ledger records 4,120 fixed32 calls, with 127,792 real rows and 4,048 padding rows. The source ran for 708 seconds including its terminal barrier, readback took 249 seconds, and the chunk completed in 959 seconds. The CUDA provider proof contains 403 neural kernel events. An ORT startup warning about a plugin device appeared alongside that successful CUDA proof.

The chunk published `COMPLETE.json`, `COMMIT_DONE.json`, and `CHUNK_ACCEPTED.json`. A local readback rechecked their links, the source and readback logs, the child, strict and ledger receipts, the digest index, and the pinned source/config hashes. The driver's strict readback checked the external bank as part of normal production. An independent external archive rehash remains pending; the local check alone does not establish that separate audit.

The new source cap is 1,500 seconds, readback cap 1,200 seconds, and chunk cap 3,000 seconds. In the normal owned flow, at most two unfinished source units can overlap a crash boundary, giving a conservative 50-minute source-work loss bound. Completed chunks are reused only after their durable markers and a future quiet-prefix revalidation. These are operating-system fsync boundaries, not a guarantee against a Windows physical power failure.

Run09's 120-index queue includes the 51 reused chunks, leaving at most 69 new chunks through index 119. At the observed source rate this is roughly a 14-hour remaining source queue, not a guaranteed 24 hours of new generation. A proposed run10 queue extension to index 239 needs a new reviewed source packet and ranked-roster extension. The next GPU handoff is planned for training once packs are ready; this record does not authorize another GPU task.

The [evidence record](https://github.com/jjoshua2/DeepFin/blob/32370b099f6d8d4ec965de135e70a752fc95a7a9/docs/experiments/evidence/2026-09-30-ceres-run09-first-durable-chunk.json) lists the local receipt and review identities by role, hash and size. Raw archives remain outside the repository.
