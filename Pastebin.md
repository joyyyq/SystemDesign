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
- Storage:
- Bandwidth:
- Memory: 80-20 rule, meaning 20% of URLs generate 80% of traffic => cache these 0%
## Step 3: System interface definition
## Step 4: Defining data model
## Step 5: High-level design
## Step 6: Detailed design
## Step 7: Identifying and resolving bottlenecks