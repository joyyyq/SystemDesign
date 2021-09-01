# Instagram
Instagram is a social networking service that enables its users to upload and share their photos and videos with other users. 

Users can choose to share information either publicly or privately.

Users can share through many other social networking platforms, such as Facebook, Twitter, Flickr, and Tumblr.

## Step 1: Requirements clarifications
### Functional Requirements:
1. users can upload/download/view photos
2. users can search based on photo/video titles
3. users can follow other users
4. system should generate and display a user's News Feed consisting of top photos from all the people the user follows
### Non-Functional Requirements:
1. highly available (practically, users can upload as many photos as they like; efficient management of storage is crucial)
2. low latency (200ms for News Feed generation)
3. consistency can take a hit in the interest of availability
3. highly reliable (never lost uploaded photo or video)

## Step 2: Back-of-the-envelope estimation
- assume 500M total users, 1M daily active users
- 2M new photos/day, 23 new photos/sec
- avg photo size = 200KB
- space/day = 2M * 200KB = 400GB
- space/10 yrs = 400GB * 365 * 10 = 1425TB

## Step 3: System interface definition

## Step 4: Defining data model
Database Schema: Photo, User, UserFollow

stoer in a distributed file storage like HDFS or S3 to enjoy the benefits offered by NoSQL

## Step 5: High-level design


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