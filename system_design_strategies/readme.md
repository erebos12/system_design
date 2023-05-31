# System Design Strategies

## General tips
- Start from the customer experience (Not from the technology) !
- Start with Non-Functional requirements !
- For whom is the software made for ? Who are the customers ? How many customers?
- What are the key use cases?
- Ask for business constraints (budget limits)
- Don't ask for requirements, dig for them !
- Improve iteratively your system design! Simplify & Optimize !
- Always balance out your system design by pros and cons !

## Scalability
- horizontal scaling (load balancing) needed ?
- mostly yes, when massive in data and requests 

## Latency
- Consider caching, CDN
- Throughput: 
  - RDBMS - Read/sec ~ 10K / Write/sec ~ 5K
  - Distributed Cache - Read/sec ~ 100K / Write/sec ~ 100K
  - Message queue - Read/sec ~ 100K / Write/sec ~ 100K
  - NoSQL - Read/sec ~ 20K-50K / Write/sec ~ 10K-25K

## Availability
- in case high availability needed, then consider following:
  - redundancy
  - data center
  - figure out single point of failures

## Data Volume
- RDBMS ~ 3TB
- Distributed Cache ~16GB - 128GB
- NoSQL - depends (consider Sharding)

## System Design Overview
- Draw your system design !
- agree on a consistent way to draw system design i.e.
  - rectangles = service, app
  - arrows for synchronous / asynchronous communication
  - user icon
  - etc.
- Agree on a standard in your team/organisation !



