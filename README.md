A high-performance, horizontally scalable key-value store written in Go that implements sharding for data distribution and replication for fault tolerance.

## Overview
This distributed key-value store is designed for high throughput and availability. It uses consistent hashing to distribute data across multiple shards, with each shard maintaining replicas to ensure data durability and availability even in the presence of node failures.


## Architecture

```mermaid
graph TD
    Client[Client Requests] --> Router[Router/Load Balancer]
    
    subgraph "Shard Management"
        Router --> ShardManager[Shard Manager]
        ShardManager --> HashFunction[Consistent Hash Function]
    end
    
    subgraph "Shard 1"
        HashFunction --> |Key Range A-H| Primary1[Primary Node 1]
        Primary1 --> |Replication| Replica1A[Replica 1A]
        Primary1 --> |Replication| Replica1B[Replica 1B]
        Primary1 -.-> |Heartbeat| Replica1A
        Primary1 -.-> |Heartbeat| Replica1B
    end
    
    subgraph "Shard 2"
        HashFunction --> |Key Range I-P| Primary2[Primary Node 2]
        Primary2 --> |Replication| Replica2A[Replica 2A]
        Primary2 --> |Replication| Replica2B[Replica 2B]
        Primary2 -.-> |Heartbeat| Replica2A
        Primary2 -.-> |Heartbeat| Replica2B
    end
    
    subgraph "Shard 3"
        HashFunction --> |Key Range Q-Z| Primary3[Primary Node 3]
        Primary3 --> |Replication| Replica3A[Replica 3A]
        Primary3 --> |Replication| Replica3B[Replica 3B]
        Primary3 -.-> |Heartbeat| Replica3A
        Primary3 -.-> |Heartbeat| Replica3B
    end
    
    style Client fill:#E9F2FF,stroke:#4A6FA5,stroke-width:1px,color:#333
    style Router fill:#C9F7FF,stroke:#1A85AD,stroke-width:1px,color:#333
    style ShardManager fill:#C9F7FF,stroke:#1A85AD,stroke-width:1px,color:#333
    style HashFunction fill:#C9F7FF,stroke:#1A85AD,stroke-width:1px,color:#333
    
    style Primary1 fill:#FFE0B2,stroke:#E67700,stroke-width:1px,color:#333
    style Primary2 fill:#FFE0B2,stroke:#E67700,stroke-width:1px,color:#333
    style Primary3 fill:#FFE0B2,stroke:#E67700,stroke-width:1px,color:#333
    
    style Replica1A fill:#E3F2FD,stroke:#1976D2,stroke-width:1px,color:#333
    style Replica1B fill:#E3F2FD,stroke:#1976D2,stroke-width:1px,color:#333
    style Replica2A fill:#E3F2FD,stroke:#1976D2,stroke-width:1px,color:#333
    style Replica2B fill:#E3F2FD,stroke:#1976D2,stroke-width:1px,color:#333
    style Replica3A fill:#E3F2FD,stroke:#1976D2,stroke-width:1px,color:#333
    style Replica3B fill:#E3F2FD,stroke:#1976D2,stroke-width:1px,color:#333
```
The system consists of the following components:

- Client Interface: Provides a simple API for put/get operations
- Router/Load Balancer: Routes requests to the appropriate shard based on the key
- Shard Manager: Manages shard assignments and handles node additions/removals
- Primary Nodes: Each responsible for a specific key range
- Replica Nodes: Maintain copies of data from primary nodes for fault tolerance

Data writes are first directed to the primary node for a key, then asynchronously replicated to replica nodes. Reads can be served by either primary or replica nodes, depending on configuration (consistency vs. availability tradeoff).

## Key Features

- Horizontal Scalability: Add more nodes to increase capacity and throughput
- Automatic Sharding: Data automatically distributed across available nodes
- Configurable Replication: Set replication factor based on reliability needs
- Fault Tolerance: System remains operational despite node failures
- Consistent Hashing: Minimizes data redistribution when scaling
- Tunable Consistency: Configure for strong or eventual consistency
- Simple API: Straightforward interface for basic operations

## Performance Metrics

![Performance Benchmark](./performance-graph-svg.svg)

## Roadmap

- [x] Raft Consensus Algorithm
  - [x] Raft Leader Election
  - [x] Raft Log Entries Append
  - [x] Raft state persistence
  
- [x] Fault-tolerant Key/Value Service
  - [x] Key/value Service Without Log Compaction
  - [x] Key/value Service With Log Compaction

- [x] Sharded Key/Value Service
