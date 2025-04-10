Architecture
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
    
    style Primary1 fill:#f96,stroke:#333,stroke-width:2px
    style Primary2 fill:#f96,stroke:#333,stroke-width:2px
    style Primary3 fill:#f96,stroke:#333,stroke-width:2px
    style Replica1A fill:#9cf,stroke:#333,stroke-width:1px
    style Replica1B fill:#9cf,stroke:#333,stroke-width:1px
    style Replica2A fill:#9cf,stroke:#333,stroke-width:1px
    style Replica2B fill:#9cf,stroke:#333,stroke-width:1px
    style Replica3A fill:#9cf,stroke:#333,stroke-width:1px
    style Replica3B fill:#9cf,stroke:#333,stroke-width:1px
    style Router fill:#bd4,stroke:#333,stroke-width:2px
    style ShardManager fill:#bd4,stroke:#333,stroke-width:2px



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
