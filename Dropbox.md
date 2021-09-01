# Dropbox
Cloud file storage enables users to store their data on remote servers. Usually, these servers are maintained by cloud storage providers and made available to users over a network (typically through the Internet). Users pay for their cloud data storage on a monthly basis.
- Availability
- Reliability and Durability
- Scalability

## Step 1: Requirements clarifications
### Functional Requirements:
1. upload and download their files/photos from any device
2. share files or folders with other users
3. automatic synchronization between devices
4. store large files up to a GB.
5. ACID-ity - Atomicity, Consistency, Isolation and Durability
6. system should support offline editing
### Extended Requirements:
1. data snapshotting allows go back to any version of the files

### Some Design Considerations
- expect huge read and write volumes
- read to write ratio is expected to be nearly the same
- Internally, files can be stored in small parts or chunks (say 4MB)
- reduce the amount of data exchange by transferring updated chunks only
- save storage space and bandwidth usage by removing duplicate chunks
- keeping a local copy of the metadata (file name, size, etc.) with the client can save us a lot of round trips to the server
- for small changes, clients can intelligently upload the diffs instead of the whole chunk

## Step 2: Back-of-the-envelope estimation
- assume 500M total users, 100M daily active users (DAU)
- assume that on avg each user connects from three different devices
- avg user has 200 files/photos => 100B total files
- avg file size = 100KB => total storage 100B * 100KB = 10PB
- 1M acive connections/minute

## Step 3: System interface definition

## Step 4: Defining data model

## Step 5: High-level design
store files and their metadata information like File Name, File Size, Directory, etc., and who this file is shared with

## Step 6: Detailed design

## Step 7: Identifying and resolving bottlenecks
### Data Partitioning and Replication
a. Range Based Partitioning: problem unbalanced DB servers
b. Hash-Based Partitioning: consistent hashing
### Cache
- How much cache memory
- Which cache eviction policy
### Load Balancer (LB)
1. Clients <-> Application servers
2. Application servers <-> database servers
3. Application servers <-> cache servers
### Purging or DB cleanup