+++
title = "LevinDB"
date = 2026-05-01T00:00:00Z
period = "May 2026"
summary = "Concurrent in-memory Key-Value store in Go designed with a 64-way sharded mutex architecture, custom TCP binary protocol, and Write-Ahead Log (WAL) for durability."
tags = ["Go", "TCP", "Mutex Sharding", "WAL", "Systems"]
+++

### Motivation & Background

Standard in-memory stores often rely on a single global lock (or standard `sync.Map` constructs) which rapidly become bottlenecks when hundreds of concurrent workers attempt writes simultaneously. I built **LevinDB** in Go to explore how far lock contention can be minimized at the architecture level while retaining durability.

---

### Architecture & Design Decisions

#### 1. 64-Way Sharded Mutex Architecture
Rather than locking the entire database state during a mutation, LevinDB hashes incoming keys and routes them across **64 independent memory shards**, each protected by its own read/write mutex. 
- Under heavy write traffic, threads targeting different key ranges operate in parallel with near-zero lock contention.

#### 2. Custom Binary Protocol over Raw TCP
Instead of using HTTP/JSON (which introduces high serialization overhead and GC allocations):
- LevinDB implements a minimal custom binary wire protocol over raw TCP sockets.
- It leverages Go's `sync.Pool` to recycle byte buffers across connections, reducing memory allocations per request and minimizing Garbage Collection pauses during traffic spikes.

#### 3. Data Durability via Write-Ahead Logging (WAL)
In-memory speed means little if a crash wipes out database state. 
- LevinDB guarantees durability by appending every write mutation to a sequential **Write-Ahead Log (WAL)** file on disk before committing it to memory.
- Upon startup, LevinDB replays the WAL to automatically restore its exact state.

---

### Key Takeaways
Building LevinDB gave me a deep, hands-on appreciation for low-level Go performance—specifically memory layout, sync primitives, TCP framing, and zero-allocation IO patterns.
