# TinyURL
URL shortening is used to optimize links across devices, track individual links to analyze audience, measure ad campaigns’ performance, or hide affiliated original URLs.

## Step 1: Requirements clarifications
### Functional Requirements:
1. generate a shorter and unique alias of the given URL
2. the short link redirect to the same place as the original link
3. users have the option to pick a custom short link
4. links expire after a standard default or user-specified timespan
### Non-Functional Requirements:
1. highly available
2. low latency 
3. secure (not guessable/predictable)
### Extended Requirements:
1. Analytics; e.g., how many times a redirection happened?
2. Accessible (through REST APIs by other services)
## Step 2: Back-of-the-envelope estimation
### Traffic: read-heavy, assume R(redirect):W(generate new short link) = 100
### Storage:
### Bandwidth:
### Memory: 80-20 rule, meaning 20% of URLs generate 80% of traffic => cache these 0%
## Step 3: System interface definition
createURL(api_dev_key, original_url, custom_alias=None, user_name=None, expire_date=None)

## Step 4: Defining data model
## Step 5: High-level design
## Step 6: Detailed design
## Step 7: Identifying and resolving bottlenecks