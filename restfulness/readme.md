# REST / Restfulness

Following sections represent only guidelines, NO rules! 
But be consistent in your design and agree on a standard.

> **Tipp**: Get familiar with _RFC7231_ (https://datatracker.ietf.org/doc/html/rfc7231)

## HTTP Methods

- GET - read
- DELETE - delete
- POST - create
- PUT - update entire resource
- PATCH - partial update

## PUT vs. PATCH

When you receive a PUT for a partial update should throw an error.
For partial updates of resource, use PATCH!

## POST and 201 & Location-Header

Snippet from RFC 7231:

> If one or more resources has been created on the origin server as a
  result of successfully processing a POST request, the origin server
  SHOULD send a 201 (Created) response containing a Location header
  field that provides an identifier for the primary resource created
  (Section 7.1.2) and a representation that describes the status of the
  request while referring to the new resource(s).

See https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.3

## Status-Codes

- 100-199 - Informational
- 200-299 - Successful
- 300-399 - Redirection
- 400-499 - Client Error
- 500-599 - Server Error

## Nested Resources

`` METHOD /<resources>/:id/<sub-resources>/:id``

Example:

`` GET /users/123/books``

`` DELETE /users/123/books/456``

> More than 2 nesting, you should maybe consider using GraphQL!

## Handling states

``PUT /users/123/enable``
``PUT /users/123/disable``

Using PUT because its idempotent. When sending multiple times ``PUT /users/123/enable``
then state does NOT change.

> Never change state in GET !

## Pagination / Sorting

``GET /<resources>?limit=X&offset=Y&sort_by=A&order_by=[asc|desc]``

Example:

``GET /books?limit=50&offset=100``

``GET /users?sort_by=email&order_by=asc``

## Idempotency

- Read https://www.rfc-editor.org/rfc/rfc7231#section-4.2.2
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
So when we execute the same POST request N times, we will have N new resources on the server. So, POST is not idempotent.

## Design Idempotent API

### Binding requests with server-generated IDs

Example: Creating job on server

1. We will first request job_id from the server. The server will create job_id and store it in the database with the current status, then return back job_id to the client.
2. Now client uses this job_id to request job execution to the server. Server checks if this job_id exists in the database and checks the status and accordingly executes the job and then returns a response to the client.
3. In this approach, we are binding requests with server-generated IDs.
4. Now if our server crashes before notifying the job execution result to the client then the client will make the same request again.
5. Now the server will check in the database if the job_id is already present in the database and confirm the execution status, after that it will send the response with the latest status and not rerun the job.
6. This is how we are using job_id as the binding key to the jobs and avoiding rerunning the job in the retry action.

### Using Idempotency-Key in request

To perform an idempotent request, provide an additional ``Idempotency-Key: <key>`` header to the request.
For more details, check 
[Idempotency Key Example](https://multithreaded.stitchfix.com/blog/2017/06/26/patterns-of-soa-idempotency-key/#:~:text=In%20the%20purchasing%20example%2C%20suppose,ID%20is%20an%20idempotency%20key).