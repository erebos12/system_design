# Protocols

## Table of Contents

1. [REST](#REST)
2. [Long Polling](#Long-Polling)
3. [WebSockets](#WebSockets)
4. [GraphQL](#GraphQL)
5. [gRPC](#gRPC)
6. [UDP](#UDP)
7. [What protocol to use](#What-Protocol-To-Use)

## REST

Following sections represent only guidelines, NO rules!
But be consistent in your design and agree on a standard.

### HTTP Methods

- GET - read
- DELETE - delete
- POST - create
- PUT - update entire resource
- PATCH - partial update

### PUT vs. PATCH

When you receive a PUT for a partial should throw an error.
For partial updates of resource, use PATCH!

### Status-Codes

- 100-199 - Informational
- 200-299 - Successful
- 300-399 - Redirection
- 400-499 - Client Error
- 500-599 - Server Error

### Nested Resources

`` METHOD /<resources>/:id/<sub-resources>/:id``

Example:

`` GET /users/123/books``

`` DELETE /users/123/books/456``

> More than 2 nesting, you should maybe consider using GraphQL!

### Handling states

``PUT /users/123/enable``
``PUT /users/123/disable``

Using PUT because its idempotent. When sending multiple times ``PUT /users/123/enable``
then state does NOT change.

> Never change state in GET !

### Pagination / Sorting

``GET /<resources>?limit=X&offset=Y&sort_by=A&order_by=[asc|desc]``

Example:

``GET /books?limit=50&offset=100``

``GET /users?sort_by=email&order_by=asc``

### Idempotency

- Read https://www.rfc-editor.org/rfc/rfc7231
- Important for retry scenarios !

- idempotent methods:
    - DELETE
    - GET
    - HEAD
    - OPTIONS
    - PUT
    - TRACE
- non-idempotent methods:
    - POST
    - CONNECT

See POST like incrementing a counter. Call it twice then 2 times increased.
So when we execute the same POST request N times, we will have N new resources on the server. So, POST is not
idempotent.

### Design Idempotent API

#### Binding requests with server-generated IDs

Example: Creating job on server

1. We will first request job_id from the server. The server will create job_id and store it in the database with the
   current status, then return back job_id to the client.
2. Now client uses this job_id to request job execution to the server. Server checks if this job_id exists in the
   database and checks the status and accordingly executes the job and then returns a response to the client.
3. In this approach, we are binding requests with server-generated IDs.
4. Now if our server crashes before notifying the job execution result to the client then the client will make the same
   request again.
5. Now the server will check in the database if the job_id is already present in the database and confirm the execution
   status, after that it will send the response with the latest status and not rerun the job.
6. This is how we are using job_id as the binding key to the jobs and avoiding rerunning the job in the retry action.

#### Using Idempotency-Key in request

To perform an idempotent request, provide an additional ``Idempotency-Key: <key>`` header to the request.
For more details, check
[Idempotency Key Example](https://multithreaded.stitchfix.com/blog/2017/06/26/patterns-of-soa-idempotency-key/#:~:text=In%20the%20purchasing%20example%2C%20suppose,ID%20is%20an%20idempotency%20key)
.

## Long Polling
HTTP Long Polling is a variation of standard polling 
that emulates a server pushing messages to a client (or browser) efficiently.
Long polling was one of the first techniques developed to allow a server to ‘push’ data to a client and 
because of its longevity, it has near-ubiquitous support in all browsers and web technologies.  
Even in an era with protocols specifically designed for persistent bidirectional communication (such as WebSockets), 
the ability to long poll still has a place as a fallback mechanism that will work everywhere.

How does it work ?

1. Requests are sent to the server from the browser, like before

2. The server does not close the connection, instead, the connection is kept open until there is data for the server to send

3. The client waits for a response from the server.

4. When data is available, the server sends it to the client

5. The client immediately makes another HTTP Long-polling request to the server

Above: HTTP Long Polling between a client and server.  Note that there is a long time between request and response as the server waits until there is data to send.

This is much more efficient than regular polling.  

- The browser will always receive the latest update when it is available

- The server is not inundated with requests that will never be fulfilled.
- 
Further reading - https://www.pubnub.com/blog/http-long-polling/

## WebSockets

- duplex protocol (2-way-protocol)
- build on top of TCP
- persistent connection
- mostly needed when your server needs to send messages actively

### Pros

- Connection is established only once (TCP connection expensive)
- real time message delivery to client i.e. instant messaging service
- server can push message, so no polling from client needed

### Cons

- more complicated to implement than HTTP, mostly stateful
- load balancer can have trouble since long term connection is used
- new "protocol" needs to be re-invented (unlike in REST)

## GraphQL
- TBC


## gRPC

- see https://grpc.io/

### Pros

- strong API contract: client & server code will be generated out of one IDL file, that's why strong consistency /
  type-safe (unlike REST)
- Binary, more efficient than JSON
- great for communication between (backend) services
- good for high throughput
- excellent support for bidirectional streaming
- language agnostic
- leverages HTTP/2 by default

### Cons

- not supported by browsers
- "protocol" needs to be re-invented (no HTTP methods)
- payload not human-readable (binary)

## UDP
- TBC

## What protocol to use

1. Do you have an external API ?
    - gRPC not supported by browser and harder to implement
    - REST, WebSocket, GraphQL, UDP, Long Polling can be an option
2. Is communication bidirectional (server needs to push messages) ?
    - prefer WebSockets or UDP
3. High throughput needed ?
    - prefer WebSockets, gRPC or UDP
4. Support for WebBrowser ?
    - No gRPC !
    - REST, GraphQL, WebSockets or Long Polling