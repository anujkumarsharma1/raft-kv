# raft-kv

A fault-tolerant key/value store in Go, built on a Raft implementation I wrote from scratch, with a fault-injection harness.

**Status:** planned, starting December 2026 after MIT 6.5840 Labs 3 and 4. The repo currently holds only a scaffold.

## What it does
Replicates a key/value store across 3 to 5 nodes. It keeps serving reads and writes when a minority of nodes crash or are partitioned, and it never returns stale or lost writes.

## How it's built
- Raft: leader election, log replication, persistence, snapshotting, membership changes.
- gRPC client API, a CLI client, Prometheus metrics.
- A test harness that randomly kills nodes and partitions the network, and a linearizability checker over the recorded history.

## How to run
    go test ./... -race
    go run ./cmd/node --id 1 --peers ...
    go run ./cmd/chaos --duration 10m

## What it measured
| Check | Result |
|---|---|
| Throughput (ops/sec), normal operation | not yet measured |
| p99 latency, normal operation | not yet measured |
| p99 latency during leader failover | not yet measured |
| Chaos run: linearizability violations found in N minutes | not yet measured |

## Bugs I hit
Write the real bug stories here as you find them: what the symptom was, how you found it, how you fixed it.
