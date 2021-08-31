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
1. highly available
2. low latency (200ms for News Feed generation)
3. consistency can take a hit in the interest of availability
3. highly reliable (never lost uploaded photo or video)

## Step 2: Back-of-the-envelope estimation
- Traffic: read-heavy, assume R(redirect):W(generate new short link) = 100
- Storage:
- Bandwidth:
- Memory: 80-20 rule, meaning 20% of URLs generate 80% of traffic => cache these 0%

## Step 3: System interface definition
explicitly state what is expected from the system

createURL(api_dev_key, original_url, custom_alias=None, user_name=None, expire_date=None)

deleteURL(api_dev_key, url_key)

## Step 4: Defining data model
- billions of records
- each small
- no relationships
- read-heavy

Database Schema: one for URL mappings, one for users

NoSQL store like DynamoDB, Cassandra or Riak - also easier to scale

## Step 5: High-level design
a. Encoding actual URL#
b. Generating keys offline (KGS) cons: single point of failutre fix: add a standby replica

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