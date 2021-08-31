# Pastebin
Pastebin like services enable users to store plain text or images over the network (typically the Internet) and generate unique URLs to access the uploaded data. 

## Step 1: Requirements clarifications
### Functional Requirements:
1. can paste data and get a unique URL to access it
2. only text
3. expire after a timespan
4. customizable
### Non-Functional Requirements:
1. reliable
2. available
3. low latency
4. secure not guessable/predictable
### Extended Requirements:
1. Analytics; e.g., how many times a paste was accessed?
2. Accessible (through REST APIs by other services)
3. limit on the amount of text user can paste at a time
4. size limits on custom URLs

## Step 2: Back-of-the-envelope estimation
- Traffic: read heavy assume 5:1
- Storage: 70% capacity model
- Bandwidth:
- Memory: 80-20 rule, meaning 20% of URLs generate 80% of traffic => cache these 0%
## Step 3: System interface definition
addPaste(api_dev_key, paste_data, custom_url=None user_name=None, paste_name=None, expire_date=None)

getPaste(api_dev_key, api_paste_key)

deletePaste(api_dev_key, api_paste_key)
## Step 4: Defining data model
- billions of records
- each metadata small (< 1KB)
- each paste object medium (a few MB)
- no relationships
- read-heavy

Database Schema: one for storing info, one for users
## Step 5: High-level design
application layer 1. serves all the read and write requests 2. talks to a storage layer to store and retrieve data

storage layer sergregates to one storing metadata while the other storing the paste contents so that they can scale individually
## Step 6: Detailed design
a. application layer
b. datastore layer
- Metadata: relational database like MySQL or a Distributed Key-Value store like Dynamo or Cassandra.
- Object storage: Amazon S3 -> when hit full capacity easily increase by adding more servers
## Step 7: Identifying and resolving bottlenecks