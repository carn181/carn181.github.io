+++
title = "LevinDB"
date = 2026-05-01T00:00:00Z
period = "May 2026"
summary = "Minimal in-memory TCP key-value database in Go with 64-way sharded mutexes, a custom binary wire protocol, persistent connections, request pipelining, and a configurable write-ahead log."
tags = ["Go", "TCP", "Key-Value Store", "Mutex Sharding", "WAL", "Pipelining", "Systems"]
+++

### What it is

**LevinDB** is a minimal in-memory key-value database I built in Go. It listens on raw TCP (`localhost:2045`), speaks a small binary protocol, and uses a write-ahead log to survive crashes.

[github.com/carn181/levindb](https://github.com/carn181/levindb)

### Why I built it

I wanted to see how much throughput I could squeeze out of a simple in-memory store by staying close to the metal: sharding the lock space so writes don't queue behind one global mutex, keeping TCP connections open for many requests, letting clients pipeline, and avoiding HTTP/JSON overhead entirely.

---

### Architecture & Design

#### 1. 64-way sharded storage

Keys are hashed with SHA-256 and routed to one of **64 independent shards**, each backed by a `map[string]string` and protected by its own `sync.RWMutex`. Threads hitting different keys rarely contend.

#### 2. Persistent, pipelined TCP connections

A single TCP connection serves many requests, so clients don't pay per-request setup. Because the protocol is strictly request-response, clients can fire off multiple requests before reading the matching responses, amortizing network round-trips.

#### 3. Binary wire protocol

Everything is framed with big-endian lengths.

- **Request header** — 9 bytes: `type (1) | key size (4) | value size (4)`
- **Response header** — 5 bytes: `status (1) | value size (4)`

Operations:

- `0` = SET
- `1` = GET
- `2` = DELETE

Response statuses:

- `0` = OK
- `1` = KEY NOT FOUND
- `2` = ERROR

#### 4. Write-ahead log with configurable durability

Every mutation is appended to `levindb.wal` before it reaches memory. On startup the log is replayed to restore state. The WAL has a magic header and a CRC32 checksum to detect corruption, and it tolerates a truncated trailing record after an unclean shutdown.

Durability is configurable via `SyncPolicy`:

- `SyncAlways` — fsync on every commit.
- `SyncEvery` — background fsync at a fixed interval; defaults to once per second, bounding loss to at most one second of writes.
- `SyncNo` — leave flushing to the OS.

---

### Quick start

```bash
go build -o bin/server ./cmd/server
go build -o bin/client ./cmd/client

./bin/server   # listens on localhost:2045
./bin/client   # interactive client
```

Run tests with:

```bash
go test ./...
```

---

### What I learned

Building LevinDB gave me hands-on experience with the full stack of a small database: binary framing, buffered TCP I/O, lock sharding, WAL replay, and the fsync durability/latency trade-off.
