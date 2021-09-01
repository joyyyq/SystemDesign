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
- assume 500M total users, 1M daily active users (DAU)
- 2M new photos/day, 23 new photos/sec
- avg photo size = 200KB
- space/day = 2M * 200KB = 400GB
- space/10 yrs = 400GB * 365 * 10 = 1425TB

## Step 3: System interface definition

## Step 4: Defining data model
Database Schema: Photo, User, UserFollow

stoer in a distributed file storage like HDFS or S3 to enjoy the benefits offered by NoSQL

## Step 5: High-level design
web servers have a connection limit => To handle this bottleneck, we can split reads and writes into separate services. 

### Reliability and Redundancy
high availability need to have multiple replicas

## Step 6: Detailed design
### Ranking and News Feed Generation
- Pre-generating the News Feed
- different approaches for sending News Feed contents to the users
1. Pull - cons: a) new data might not be shown to the users until clients issue a pull request b) most of the time, prs will result in an empty response if there's no new data
2. Push - cons: a user who follows a lot of people or a celebrity user who has millions of followers
3. Hybrid
### News Feed Creation with Sharded Data
- need a mechanism to sort photos on their time of creation. To efficiently do this, we can make photo creation time part of the PhotoID. We can use epoch time for this.

## Step 7: Identifying and resolving bottlenecks
### Data Sharding
a. Partitioning based on UserID
- each DB shard has its own auto-increment sequence for UserIDs, and since we will append ShardID with each UserID. it will make it unique throughout our system
- hot users?
- non-uniform distribution of storage
- can't store all pics of a user on one shard?
- can cause unavailability if that shard is down
b. Partitioning based on PhotoID
- dedicate a separate database instance to generate ato-incrementing IDs
### Cache
- push its content closer to the user using a large number of geographically distributed photo cache servers and use CDNs
- a cache for metadata servers to cache hot database rows
- use Memcache to cache the data, and Application servers before hitting the database can quickly check if the cache has desired rows
- LRU