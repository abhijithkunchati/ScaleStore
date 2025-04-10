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
## Performance Metrics

![Performance Benchmark](./performance-graph-svg.svg)

# MIT 6.824 Distributed Systems Labs

### (Updated to Spring 2020 Course Labs)

Course website: http://nil.csail.mit.edu/6.824/2020/schedule.html

- [x] Lab 1: MapReduce

- [x] Lab 2: Raft Consensus Algorithm
  - [x] Lab 2A: Raft Leader Election
  - [x] Lab 2B: Raft Log Entries Append
  - [x] Lab 2C: Raft state persistence
  
- [x] Lab 3: Fault-tolerant Key/Value Service
  - [x] Lab 3A: Key/value Service Without Log Compaction
  - [x] Lab 3B: Key/value Service With Log Compaction

- [x] Lab 4: Sharded Key/Value Service
