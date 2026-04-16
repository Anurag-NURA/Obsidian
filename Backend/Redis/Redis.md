It is an in-memory data store.

## What Problem does Redis solves ?
Whenever a Client interacts with a Server the server (API) interacts with Database to fulfill the request made by the client. This process can be done by Data Query. Now Data query can be complex where data is retrieved from data tables or fetched by looking up from different foreign tables.

Lets say the same Client refreshes the application the entire process will be repeated which is:
+ becomes unnecessary request from user
+ increases  Response time (*reading time and user waiting time*)
+ becomes very costly to deliver the same service (*on every refresh*)

### Redis brings the solution:
Redis solves all these problems by caching the data. Redis also stores [[Computed Data]] which can save time and unnecessary computation. 

## Data types
1. [[Redis Strings]]
2. [[Redis List]]
3. [[Redis Sets]]
4. [[Redis JSON]]