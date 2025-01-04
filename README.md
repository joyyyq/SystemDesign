# System Design
- Step 1: Requirements clarifications
- Step 2: Back-of-the-envelope estimation
- Step 3: System interface definition
- Step 4: Defining data model
- Step 5: High-level design
- Step 6: Detailed design
- Step 7: Identifying and resolving bottlenecks

## Delivery Framework
### Requirements
1. Functional Requirements
Users/Clients should be able to ...
2. Non-functional Requirements
The system should be able to ...
- CAP Theorem
- Environtment Constraints
- Scalability
- Latency
- Durability
- Security
- Fault Tolerance
- Compliance
3. Capacity Estimation
### Core Entities
### API or Systme Interface
- RESTful API
- GraphQL API
- Wire Protocol
### [Optional] Data Flow
### High Level Design

## Core Concepts
### Scaling
#### Work Distribution
keep load on the system as even as possible
#### Data Distribution
### Consistency
Consistency, at the highest level, pertains to how much your users can tolerate getting stale data. A strongly consistent system will ensure that, after the data is written, all subsequent reads will reflect that write. A weakly consistent or more commonly eventually consistent system will not make this guarantee, instead allowing for a period of time where the data is stale.
### Locking
#### Granularity of the lock
We want locks to be as fine-grained as possible.

#### Duration of the lock
We want locks to be held for as short a time as possible. 

#### Whether we can bypass the lock
In many cases, we can avoid locking by employing an "optimistic" concurrency control strategy, especially if the work to be done is either read-only or can be retried. In an optimistic strategy we're going to assume that we can do the work without locking and then check to see if we were right. In most systems, we can use a "compare and swap" operation to do this.

### Indexing
do a minimal amount of up-front work so that your reads can be extra fast.
#### Indexing in Databases
##### Specialized Indexes

ElasticSearch is our recommended solution for these secondary indexes, when it can work. ElasticSearch supports full-text indexes (search by text) via Lucene, geospatial indexes, and even vector indexes. You can set up ElasticSearch to index most databases via Change Data Capture (CDC) where the ES cluster is listening to changes coming from the database and updating its indexes accordingly. This isn't a perfect solution! By using CDC, you're introducing a new point of failure and a new source of latency, the data read out of your search index is going to be stale, but that may be ok.

### Communication Protocols
