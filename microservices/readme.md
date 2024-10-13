# Microservice Architecture

Table of Content

1. [When to use Microservice Architecture](#When-to-use-Microservice-Architecture)
2. [Bounded Context](#Bounded-Context)
3. [Design Strategies](#Design-Strategies)
4. [Microservice Patterns](#Microservice-Patterns)
5. [Microservice Data Consistency](#Microservice-Data-Consistency)
6. [Links](#Links)

See also https://microservices.io/post/architecture/2023/02/09/assemblage-architecture-definition-process.html

## When to use Microservice Architecture
- Business teams are separated teams (as per departments) such as Product, Sales, Payment etc.
  - Also organizational change in future will come up. So new business teams will pop up.
- Innovate and experiment with new features as soon as possible
  - i.e. Product team wants to test a new feature independently from other departments
  - so deployment should be independent from other teams
- Flexible scaling of single components/departments
  - more load on product search, which means scale only product components, not the others
  - for instance more users are searching products but they don't buy more, so no scaling in payment needed
- Technology agnostic approach
  - tech teams should be able to use different tech-stacks for their services
  - this is the foundation for tecnical *innovation*

## Bounded Context

Each microservice typically owns its own data,
meaning that the tables belonging to a particular service are only
accessed by that service. For example, a Wishlist service might own
its corresponding wishlist tables. If other services need wish list
data, those services would have to ask the Wishlist service for that
information rather than accessing the wishlist tables directly.
This concept is known as a bounded context, a term coined by Eric
Evans in his book Domain-Driven Design (Addison-Wesley). Within
the scope of microservices, this means that all of the source code
representing some domain or subdomain (such as a wish list for a customer), along with the corresponding data structures and data,
are all encapsulated as one unit.

## Design Strategies

Microservice Architecture: https://microservices.io/patterns/microservices.html

Main considerations:
- [Microservice Decomposition](#Microservice-Decomposition)
- [Communication](#Communication)
- Data Managment
- Transaction Management
- Deployments
- Resilience

### Microservice Decomposition

> Tip: Start with the organizational structure. 
Ask questions like: 
  - How is the organization it structured? 
  - What business teams/departments exist and how do they work with each other (i.e. Product, Order, Payment team) ?

#### Decompose by sub-domains (*Bounded Context*)
  - Conduct 'Domain Driven Design'
    - INPUT: functional requirements such as user-stories
    - OUTPUT:  "Object Relationship Diagram" which gives us *Bounded-Contexts*
  - *Bounded-Context* could be: Customers, Orders, Payment and Shopping Cart
  - Now identify *"Bounded-Context Boundaries"* by the entities/objects used in a specific Bounded-Contexts:
    - Customers: Customer, Address, Companies, Account
    - Orders: Customer, Order, Items, History
    - Payment: Payers, Payments, Adress
    - Shopping cart: Users, Cart, Items, Prices
      
      ==> Overlappings & Redundancies are important !!!
- Identify microservices:
  - Microservices should NOT use too many entities (see *"Bounded-Context Boundaries"*)
  - NOT TOO SMALL & NOT TOO BIG
  - when one microservice use ALL entities, then it gets to complex (too big)
  - For instance a Customer microservice only uses Customer data such as name & address and the Payment service only use paymant data such as credit card, bank account
  - But it can also be possible that the Customer service uses also the payment data for a customer. So then only one microservice is needed! You need to balance this out.
  - one microservice only for the credit-card might me TOO SMALL

### Communication

What type of communication - Sync/Async

- Non-Blocking / Async Approach:
    - using AMQP (Advanced Message Queuing Protocol)
    - Kafka or RabbitMQ
    - one-to-one 
      - only 1 producer <-> queue <-> 1 consumer
    - one-to-many 
      - 1 producer <-> queue <-> n consumers
      - uses Topic model

What protocols to choose 
- see https://github.com/erebos12/system_design/tree/main/protocols

Avoid direct communication from client-apps to microservices! Use API-Gateway and/or Orchestrator services.


## Microservice Patterns 

See https://microservices.io/index.html !!!

### Database-per-Service-Pattern

See [Bounded Context](#Bounded-Context). Each microservice owns its data.

### Polyglot Persistence

Different database types for different service possible. 
For instance:
- Document store (NoSQL)
- Key-Value store
- Relational Database
- Graph Database

Also evaluate following aspects:
- Using API composition and/or 
- CQRS (Command and Query Responsibility Segregation) 
  - pattern that separates read and update operations for a data store)

### API Gateway Pattern: Your One-Stop-Shop for Microservices

#### Responsibilities of an API Gateway

- API Composition (for simple data queries) - see https://microservices.io/patterns/data/api-composition.html
- Routing 
- Load Balancing
- Circuit Breaker
- Authentication and Authorization
- SSL Certificate
- Logging
- Protocol translation
- Rate Limiting
- Token Managment
- Billing
- Analytics, Alerting, Monitoring and Statistics
- Cache Management

> **_Be careful with Gateway Routing Pattern !_**

> A widely used way of an API Gateway is that it calls different backend-services for fetching data. Then it combines the received data into one data structure and returns it to the client. This functionality is what the API Gateway service is usually responsible for. 
This pattern is very common in microservices architecture and 
works in most cases related to fetching data for serving GET requests (easy logic). 
**_But it is very limited when you have to apply business logic. Does the business logic grow and gets more and more complex, then it’s usually not a functionality of the Gateway service!!! In this case a dedicated microservice should handle those kind of logic, NOT the API-Gateway_**.

**Microservices Authentication and Authorization Using API Gateway**

See Medium article https://medium.com/permify-tech-blog/microservices-authentication-and-authorization-using-api-gateway-b04c058bf00f

### Backends for Frontends Pattern - BFF

- seperate API for specific frontend application
- For example you can have dedicated API Gateways responsible for mobile, web and desktops apps
- when API Gateway for desktops app fails the mobile and web apps are not affected (no single-point-of-failure)
- you can independently scale API gatewayx when its needed, i.e. multiple API gateways for mobile apps but not for web apps



### Service Discovery Pattern: Navigating the Microservices Maze with Ease

- Server Side discovery (Load Balancer, Cluster Solution like Kubernetes)
- Client Side discovery

### Circuit Breaker Pattern: Shield Your Microservices from Cascading Failures

### Load Balancing Pattern: Distribute Traffic Efficiently for High-Performance Microservices

### Bulkhead Pattern: Fortify Your Microservices with Advanced Fault Isolation

### CQRS Pattern: Boost Your Microservices Performance with Separation of Concerns

### Event-Driven Architecture Pattern: Empower Your Microservices with Real-Time Responsiveness

### Saga Pattern: Tackle Distributed Transactions with Confidence

### Retry Pattern: Boost Your Microservices Resilience with Graceful Error Recovery

### Backends for Frontends Pattern (BFF): Optimize User Experience with Tailored Service Aggregation

### Sidecar Pattern: Supercharge Your Microservices with Modular Functionality

### Strangler Pattern: Transform Your Monolith into Microservices with Confidence

### Microservices communication: Fetching data from another service

See https://blog.devgenius.io/microservices-communication-fetching-data-from-another-service-7eed741bc070

1. Direct call to the other service
2. Embedded library
3. Local data projection

## Microservice Data Consistency
- https://dilfuruz.medium.com/data-consistency-in-microservices-architecture-5c67e0f65256
- https://www.baeldung.com/cs/saga-pattern-microservices


## Links

**Top 10 Microservices Design Patterns you should know** - https://medium.com/@sylvain.tiset/top-10-microservices-design-patterns-you-should-know-1bac6a7d6218
