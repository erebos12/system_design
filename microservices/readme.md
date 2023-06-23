# Microservice Architecture

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

See https://microservices.io/post/architecture/2023/02/09/assemblage-architecture-definition-process.html

## Microservice Data Consistency
- https://dilfuruz.medium.com/data-consistency-in-microservices-architecture-5c67e0f65256
- https://www.baeldung.com/cs/saga-pattern-microservices


## Microservice Patterns 

See https://microservices.io/index.html !!!

### API Gateway Pattern: Your One-Stop-Shop for Microservices

#### Responsibilities of an API Gateway

- API Composition (for simple data queries) - see https://microservices.io/patterns/data/api-composition.html
- Routing 
- Service discovery
- Authentication and security policy enforcements
- Protocol translation
- Rate Limiting
- Billing
- Analytics, Alerting, Monitoring and Statistics
- Cache Management

> **_Attention_**!
> Another way is to have a separate service that calls all the source services, 
fetching data from each of them. Then it combines the received data into one data structure and 
returns it to the client. This functionality is what the API Gateway service is usually responsible for. 
This pattern is very common in microservices architecture and 
works in most cases related to fetching data for serving GET requests. 
**_But it is very limited when you have to apply business logic and, usually, 
it’s not a functionality of the Gateway service_**, as all the domain-related logic 
is contained in the dedicated microservice.

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

## Reviewing Microservice Architecture

https://chrisrichardson.net/consulting-review.html

## Microservice - Data Patterns

### Database per Service

- Using API composition and/or 
- CQRS (Command and Query Responsibility Segregation) 
  - pattern that separates read and update operations for a data store)

### Shared database
- TBC