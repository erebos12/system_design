# REST / Restfulness

Following items are only guidelines, NO rules! 
But be consistent your design and agree on a standard.

## HTTP Methods

- GET - read
- DELETE - delete
- POST - create
- PUT - update entire resource
- PATCH - partial update

## PUT vs. PATCH

When you receive a PUT for a partial should throw an error.
For partial updates of resource, use PATCH!

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

- Read https://www.rfc-editor.org/rfc/rfc7231

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



