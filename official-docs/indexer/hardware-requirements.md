# Hardware requirements

In the following, you can find the hardware requirements to participate in the network as an Indexer.

| **Setup**    | Postgres  (CPUs) | Postgres  (memory in GB) | Postgres  (disk in TBs) | VMs  (CPUs) | VMs  (memory in GB) |
| ------------ | ---------------- | ------------------------ | ----------------------- | ----------- | ------------------- |
| **Small**    | 4                | 8                        | 1                       | 4           | 16                  |
| **Standard** | 8                | 30                       | 1                       | 12          | 48                  |
| **Medium**   | 16               | 64                       | 2                       | 32          | 64                  |
| **Large**    | 72               | 468                      | 3.5                     | 48          | 184                 |

> **Small** = enough to get started with indexing several subgraphs\
> **Standard** = default setup\
> **Medium** = required for indexing 100 subgraphs and performing 200-500 requests per second\
> **Large** = Required for indexing all currently used subgraphs and serving requests for the related traffic
