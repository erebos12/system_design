# Databases

## Indexes
- similar to table of content (index) in books
- index is column-wise

### Data Structure of Indexes
- need to be handy also for non-exact matches like name='a name', 
so maybe HashMap is not the best data structure
- uses B-Tree (especially B-Tree+) - see data structure for that
  - leafs are connected to each other

## Sharding

### Tenant-based sharding (geo-sharding)
  - per country for instance but uneven distribution can happen
  - big shards can still happen and could be too big to handle though

### Hash-based sharding
  - when no clear separation possible, then using hash to define what shard
  - i.e. 4 shards/databases, then hash(ID)%4
  - even distribution for sharding by this approach
  - but adding new shards can be complicated, that's why not good when DB grows quickly
  - no foreign keys, so not that good for relational data
  - adding new shards requires re-sharding which can be very expensive -> "Consistent Hashing"
  - cross-shard operations can be expensive
  - 'Locator Service' or 'Shard Router' might  be in between to locate our dataset for us
    - easier to add new shards
    - but single point of failure and must be super reliable

> BE CAREFUL WITH SHARDING ! It can be complicated and could increase complexity significantly!

### Consistent Hashing

- can avoid re-sharding
- using range of hashes (0-X => shard 1 / X+1-Y => shard 2 etc.)

