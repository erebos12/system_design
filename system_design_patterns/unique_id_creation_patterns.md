# Unique ID creation patterns


## Requirements to unique IDs
We can have different requirements for a unique Id depending upon the service. For e.g.

- Any random Unique ID of some fixed size (Like a unique tiny url/link of 7 characters)
- Unique Id’s in sequential order (Database auto-incrementing primary key)
- Unique Id with some fixed size and being sortable (Tweets Id, Instagram image id’s etc.)

### GUIDs / UUIDs

Read - https://en.wikipedia.org/wiki/Universally_unique_identifier

GUIDs are large, enormous numbers that are nearly guaranteed to be unique. They are usually 128 bits long and look like this in hexadecimal:

30dd879c-ee2f-11db-8314-0800200c9a66

The format is a well-defined sequence of 32 hex digits grouped into chunks of 8–4–4–4–12. This gives us 2^128 or about 10^38 numbers.

But problem with GUIDs are that there can be collisions howsoever minuscule that probability is.

Moreover, they have 128 bits (Our requirement is shorter bit size of 64).

FurtherMore, by default (Random GUIDs) they are not sortable (Though we can have Time-based GUID which are based on the current time)

### ObjectID’s of MongoDB
We can leverage ObjectId value of MongoDB as a GUID. The 12-byte ObjectId (96-bits)value consists of:

- 4-byte timestamp value, representing the ObjectId’s creation, measured in seconds since the Unix epoch
- 5-byte random value
- 3-byte incrementing counter, initialised to a random value
For e.g. 507c7f79bcf86cd7994f6c0e has ISO time value of 2012–10–15T21:26:17Z

ObjectID’s of MongoDB are time sortable but they are longer than 64 bits (Total 96 bits). Thus, they consume a bigger space ( In database as storage, then in indexes and also if ObjectId is used as key in caching). 
This makes ObjectId not suitable for service where key size is limited to 64 bit or less.

### Ticker Server — Flickr Ticketing Service
We can use unique sequential 64 bit ID’s (32 bits are also a possibility) by using a SQL table and it’s auto-increment feature for primary key. So whenever we request our service for new Id, we can simply call INSERT ON DUPLICATE KEY UPDATE. This allows us to atomically update in place a single row in a database, and get a new auto-incremented primary ID.

Since these Id’s are sequential they are naturally sortable. Moreover, we can limit Id size to 32 or 64 bits.

However, this approach has following drawbacks :

a.) Since there is only single database this becomes a single point of failure (If for some reason database is not available our system could come to a halt)

b.) Our design is not scalable. We might breach write limits in case they are too many requests for unique ids in a very short span of time

To make this design scalable we can horizontally shard our SQL table to multiple database servers. For e.g. we can create two ticket servers (With two different SQL backends) for “High Availability” and to cater for Single point of failure we can round robin requests to these servers.

However, the downside of this solution is that we can get two same ids from these two ticket servers. One way to handle Id collision is to make sure that both servers create different kind of ids (One even and another odd)

TicketServer1:
auto-increment-increment = 2
auto-increment-offset = 1

TicketServer2:
auto-increment-increment = 2
auto-increment-offset = 2
A limitation of above scaling approach is that we lose sorbability of ids. For eg. if one id of TicketServer1 is say 101 and another id of TicketServer2 is say 202 , we cannot be sure of which one is created first (AsTicketServer2202 could have got created earlier than 101 on TicketServer1 but number comparison tells us otherwise)

In nutshell , usage of using a single DataBase becomes single point of failure( Flickr reported that, even at huge scale, it has never caused an issue).

Usage of multiple DataBases, can no longer guarantee that they are sortable over time.

Snowflake from Twitter
To create 64 bit ids which are time sortable and can be created at large scale, twitter proposed snowflake. To generate the roughly-sorted (As ID generation servers cannot have the same clock to generate the timestamp) 64 bit ids in an uncoordinated manner, they settled on a composition of: timestamp, worker number and sequence number. Since we can have upto 1024 machines this approach is scalable and also doesn’t have single point of failure.

An Id is composed of:

Time — 41 bits (millisecond precision w/a custom epoch of Twitter gives 69 years)
Configured machine id — 10 bits — gives us up to 1024 machines
Sequence number — 12 bits — rolls over every 4096 per machine (with protection to avoid rollover in the same ms)
1 bit is reserved for future use and value is set as 0
Pros :
– Snowflake IDs are 64-bits, half the size of a UUID
– Can use time as first component and remain sortable
– Distributed system that can survive dying nodes

Cons:
This design requires Zookeeper to keep mapping of Nodes and Machine Ids. Also it requires several Snowflake servers and introduces additional complexity and more ‘moving parts’ .

### Instagram Id generation
Instagram used the same approach as Twitter’s snowflake when it comes to composition of ids :

41 bits for time in milliseconds (gives us 41 years of IDs Instagrams custom epoch)
13 bits that represent the logical shard ID
10 bits that represent an auto-incrementing sequence, modulus 1024. This means we can generate 1024 IDs, per shard, per millisecond
Let’s first see how Instagram combines these fields to generate a time sortable 64 bit ids. Then we will see how Instagram id generator approach avoids requirement of a Zookeeper to mapping of Node Id (Or shard Id) with machine Id.

let’s say it’s September 9th, 2011, at 5:00pm and Instagrams ‘epoch’ begins on January 1st, 2011. There have been 1387263000 milliseconds since the beginning of their epoch, so to start the ID, let’s fill the left-most 41 bits with this value with a left-shift:

id = 1387263000 <<(64-41)
Next, let’s take the shard ID for this particular piece of data we’re trying to insert. Let’s say we’re sharding by user ID, and there are 2000 logical shards; if user ID is 31341, then the shard ID is 31341 % 2000 -> 1341. We fill the next 13 bits with this value:

id |= 1341 <<(64-41-13)
Finally, let’s take whatever the next value of auto-increment sequence (this sequence is unique to each table in each schema) and fill out the remaining bits. Let’s say we’d generated 5,000 IDs for this table already; our next value is 5,001, which we take and mod by 1024 (so it fits in 10 bits) and include it too:

id |= (5001 % 1024)
This gives the final id which has 41 bits of timestamp and is sortable by time.

Instagram sharded it system into several thousand ‘logical’ shards that are mapped in code to far fewer physical shards.

With this approach, they can start with just a few database servers, and eventually move to many more, simply by moving a set of logical shards from one database to another, without having to re-bucket any of their data.

They used Postgres’ schemas feature to make this easy to script and administrate (Without using Zookeeper)

Postgres’ Schemas (not to be confused with the SQL schema of an individual table) are a logical grouping feature in Postgres.

Each Postgres DB can have several schemas, each of which can contain one or more tables. Table names must only be unique per-schema, not per-DB, and by default Postgres places everything in a schema named ‘public’.

Each ‘logical’ shard is a Postgres schema in our system, and each sharded table exists inside each schema.

ID creation is delegated to each table inside each shard, by using PL/PGSQL, Postgres’ internal programming language, and Postgres’ existing auto-increment functionality. This way Instagram scales this architecture.

### ID-Creator service from ranges

A service creates an ID from a fixed range for each client. So each client gets a range assigned from which the ID is created for this 
specific client. 