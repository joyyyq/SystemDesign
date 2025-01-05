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
- internal (for a typical microservice application consistitues 90%+ of system design problems) 
- external

who initiates the communication, what are the latency considerations, and how much data needs to be sent.

- HTTP(S) request is statless, can scale API horizontally by placing it behind a load balancer
- Long polling near-realtime updatess
- Websockets realtime, bidirectional communication 
- Server Sent Events(SSE)
more efficient for unidirectional communication from the server to the client
achieve thru a single, long-lived HTTP connection

### Security
#### Authentication / Authorization

#### Encryption

#### Data Protection

### Monitoring
#### Infrastructure Monitoring
- CPU usage, memory usage, disk usage, and network usage
#### Service-Level Monitoring
- request latency, error rates, and throughput
#### Application-Level Monitoring
- number of users, number of active sessions, and number of active connections

## Key Technologies
### Core Database
#### Relational dbs
##### What is a relational db and when should you use it? 
the most common type of db
often used for transactional data 
##### Things you should know about relational databases
1. SQL Joins
2. Indexes
3. RDBMS Transactions
##### What are the most common relational databases? 
Postgres and MySQL
#### NoSQL dbs 
##### What is a NoSQL database and when should you use it?
- key-value, document, column-family, and graph formats
- schema-less
- unstructured, semi-structured, or structred data.
###### Flexible Data Models
###### Scalability
###### Handling Big Data and Real-Time Web Apps 
##### Things you should know about NoSQL databases
1. Data Models
2. Consistency Models
3. Indexing 

the most common types of indexes are B-Tree and Hash Table Indexes
4. Scalability
consistent hashing and/or sharding
##### What are the most common NoSQL dbs? 
DynamoDB and MongoDB

#### Blob Storage
##### What is blob storage and when should you use it?
some common examples
- Design Youtube -> Store videos in blob, metadata om db
- Design Instagram -> Store images & videos in blob, store metadata in db
- Design Dropbox -> Store files in blob, store metadata in a db  
##### Things you should know about blob storage
1. Durability
2. Scalability
3. Cost
4. Security
5. Upload and Download Directly from the Client
6. Chunking
##### Examples of blob storage services
Amazon S3 and Google Cloud Storage

#### Search Optimized Database
##### What is a search optimized database and when should you use it?
eg. Ticketmaster and Twitter
##### Things you should know about search optimized Databases
1. Inverted Indexes
2. Tokenization: break a peice of text into individual words
3. Stemming: reduce words to their room form
4. Fuzzy Search: tolerace slight misspelling or variations in the search term (edit distance caulculation)
5. Scaling
##### Examples of search optimized Databases
The clear leader in this space is Elasticsearch. Elasticsearch is a distributed, RESTful search and analytics engine that is built on top of Apache Lucene. It is designed to be fast, scalable, and easy to use. It is the most popular search optimized database and is used by companies like Netflix, Uber, and Yelp. Elasticsearch has hosted offerings like Elastic Cloud and AWS OpenSearch which make it easy to get started.

#### API Gateway
##### What is an API gateway and when should you use it?
##### What are the most common API gateways?
AWS API Gateway, Kong, and Apigee

#### Load Balancer
###### What is a load balancer and when should you use it?
###### What are the most common load balancers?
AWS Elastic Load Balancer, NGINX, and HAProxy.

#### Queue 
###### What are queues and when should you use them?
common use cases
1. Buffer for Bursty Traffic
2. Distribute Work Across a System
###### Things you should know about queues 
1. Message Ordering
2. Retry Mechenisms
3. Dead Letter queues
4. Scaling with Partitiions
5. Backpressure
###### What are the most common queueing technologies?
Kafka and SQS 

#### Streams/Event Sourcing
##### What are streams and when should you use them?
