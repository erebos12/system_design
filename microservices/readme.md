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

## Microservice Data Consistency
- https://dilfuruz.medium.com/data-consistency-in-microservices-architecture-5c67e0f65256
- https://www.baeldung.com/cs/saga-pattern-microservices


## Microservice Patterns 

### API Gateway Pattern: Your One-Stop-Shop for Microservices

### Service Discovery Pattern: Navigating the Microservices Maze with Ease

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

