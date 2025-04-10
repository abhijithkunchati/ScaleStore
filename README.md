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
<svg viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg">
  <!-- Background -->
  <rect width="800" height="400" fill="#f8f9fa" rx="5" ry="5"/>
  
  <!-- Title -->
  <text x="400" y="30" text-anchor="middle" font-family="Arial" font-size="20" font-weight="bold">Key-Value Store Performance</text>
  
  <!-- Axes -->
  <line x1="50" y1="350" x2="750" y2="350" stroke="#333" stroke-width="2"/>
  <line x1="50" y1="350" x2="50" y2="50" stroke="#333" stroke-width="2"/>
  
  <!-- X-axis labels -->
  <text x="150" y="375" text-anchor="middle" font-family="Arial" font-size="12">1 Shard</text>
  <text x="300" y="375" text-anchor="middle" font-family="Arial" font-size="12">3 Shards</text>
  <text x="450" y="375" text-anchor="middle" font-family="Arial" font-size="12">5 Shards</text>
  <text x="600" y="375" text-anchor="middle" font-family="Arial" font-size="12">10 Shards</text>
  
  <!-- Y-axis labels -->
  <text x="45" y="350" text-anchor="end" font-family="Arial" font-size="12">0</text>
  <text x="45" y="280" text-anchor="end" font-family="Arial" font-size="12">25K</text>
  <text x="45" y="210" text-anchor="end" font-family="Arial" font-size="12">50K</text>
  <text x="45" y="140" text-anchor="end" font-family="Arial" font-size="12">75K</text>
  <text x="45" y="70" text-anchor="end" font-family="Arial" font-size="12">100K</text>
  
  <!-- Grid lines -->
  <line x1="50" y1="280" x2="750" y2="280" stroke="#ddd" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="50" y1="210" x2="750" y2="210" stroke="#ddd" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="50" y1="140" x2="750" y2="140" stroke="#ddd" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="50" y1="70" x2="750" y2="70" stroke="#ddd" stroke-width="1" stroke-dasharray="5,5"/>
  
  <!-- Throughput line -->
  <polyline 
    points="150,320 300,245 450,175 600,100" 
    fill="none" 
    stroke="#3498db" 
    stroke-width="3"/>
  
  <!-- Throughput data points -->
  <circle cx="150" cy="320" r="5" fill="#3498db"/>
  <circle cx="300" cy="245" r="5" fill="#3498db"/>
  <circle cx="450" cy="175" r="5" fill="#3498db"/>
  <circle cx="600" cy="100" r="5" fill="#3498db"/>
  
  <!-- Replication factor line -->
  <polyline 
    points="150,315 300,285 450,230 600,180" 
    fill="none" 
    stroke="#e74c3c" 
    stroke-width="3"/>
  
  <!-- Replication data points -->
  <circle cx="150" cy="315" r="5" fill="#e74c3c"/>
  <circle cx="300" cy="285" r="5" fill="#e74c3c"/>
  <circle cx="450" cy="230" r="5" fill="#e74c3c"/>
  <circle cx="600" cy="180" r="5" fill="#e74c3c"/>
  
  <!-- Legend -->
  <rect x="600" y="50" width="140" height="70" fill="white" stroke="#ddd" rx="5" ry="5"/>
  <circle cx="620" cy="75" r="5" fill="#3498db"/>
  <text x="635" y="80" font-family="Arial" font-size="12">Throughput (ops/s)</text>
  <circle cx="620" cy="100" r="5" fill="#e74c3c"/>
  <text x="635" y="105" font-family="Arial" font-size="12">With Replication</text>
  
  <!-- X-axis label -->
  <text x="400" y="395" text-anchor="middle" font-family="Arial" font-size="14">Number of Shards</text>
  
  <!-- Y-axis label -->
  <text x="15" y="200" text-anchor="middle" font-family="Arial" font-size="14" transform="rotate(-90,15,200)">Operations per second</text>
</svg>
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
