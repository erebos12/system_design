# System Design Strategies

## General Tips

> Don't ask for requirements, dig for them !

> Improve iteratively your system design! Simplify & Optimize !

> Always balance out your system design by pros and cons !

## How to start a system design

### 1. Start from the users perspective

- For whom is the software made for ?
- Do you have different kind of users ?
    - Uber: Riders & Drivers
    - Ebay: Buyers & Sellers
- How many of them will be expected per time interval ?
    - i.e. 100K per month

### 2. Ask for Non-Functional requirements
- Ask for expected data volume / capacity to derive the Storage requirement
  - See [Example](#Example-to-derive-storage-requirements-for-DB)
- Ask for expected request rate (reads/writes per time interval)
  - See [Example](#Example-to-figure-out-writes-per-second)
  - See [Throughput](#Throughput)
- Ask for Availability requirements - [Availability](#Availability)
- Ask for Scalability requirements - [Scalability](#Scalability)

### 3. What are the key use cases
- concentrate on the most important use-cases first
  - searching, playing, buying, selling etc.
- later you can dig deeper for other use-cases

## Scalability

- horizontal scaling (load balancing) needed ?
- mostly yes, when massive in data and requests

## Throughput
- Ask first for average load and then for spikes/peaks
  - Result: X requests per second (avg/worst/best)
- Throughput:
    - RDBMS - Read/sec ~ 10K / Write/sec ~ 5K
    - Distributed Cache - Read/sec ~ 100K / Write/sec ~ 100K
    - Message queue - Read/sec ~ 100K / Write/sec ~ 100K
    - NoSQL - Read/sec ~ 20K-50K / Write/sec ~ 10K-25K
- Consider caching and/or CDN

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

## Example to figure out writes per second

Assumption: 600 Mio requests per month (600 is better to calculate)

- 600M / 30 days = 20M per day
- 20M rounding up to ~24M / 24 hours = 1M per hour
- 1M rounding up to ~1.2M / 60 min = 20K per minute
- 20K rounding down to ~18K / 60 sec = 300 per second

=> Result: 300 writes per second

## Example to derive storage requirements for DB

Note: Just an example. The numbers can be changed as needed!

For instance to determine the storage requirement for a URL shortener, could look like that:

Assumption: 30 billion URLs in total to store

- Each URL has 100 bytes in average
- 30 billion urls * 100 bytes = 3 Trillion bytes = 3 Billion GB = 3 Million MB = 3 GB


=> Result: 3 GB 
