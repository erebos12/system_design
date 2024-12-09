# Event Driven Architecture

Event-Driven Architecture (EDA) is a software design pattern in which the flow of the program is determined by events, which can be messages, state changes, or any type of significant occurrence. This architecture is widely used in distributed systems, microservices, and real-time data processing applications, as it allows services and components to react to events asynchronously.

Here are the key facts about Event-Driven Architecture:

### 1. **Events as Primary Entities:**
   - In EDA, an event is a significant change in the system's state. Examples include a user making a purchase, a sensor detecting a temperature change, or an order being shipped. These events are generated by producers and consumed by one or more consumers.
   - Events are typically immutable: they describe something that has happened and can't be changed retroactively.

### 2. **Event Producers and Consumers:**
   - **Event Producers**: These are components that detect or create events. For example, in an e-commerce system, the checkout process might generate an event for an order being placed.
   - **Event Consumers**: These components listen for specific events and react to them. A payment service might react to the "Order Placed" event by processing the payment.

### 3. **Asynchronous Communication:**
   - Components in EDA communicate asynchronously. Event producers don’t wait for consumers to process events; instead, they publish the event and move on. This decouples the producers and consumers, allowing for greater flexibility and scalability.
   - This is often implemented using message brokers (like Apache Kafka, RabbitMQ, or AWS SNS/SQS), which mediate between the producers and consumers.

### 4. **Loose Coupling:**
   - Event-driven systems promote loose coupling between components. Producers of events are unaware of who is consuming their events, and consumers only care about the events they are interested in. This allows independent evolution of services.

### 5. **Real-Time Processing:**
   - One of the main benefits of EDA is real-time or near real-time processing. Systems can respond to events as they happen, which is useful in scenarios such as monitoring, analytics, IoT systems, and fraud detection.

### 6. **Scalability:**
   - EDA naturally supports scaling because event producers and consumers can be independently scaled based on load. You can have multiple consumers handling events in parallel without affecting the producers.

### 7. **Complex Event Processing (CEP):**
   - EDA often involves processing multiple events over time to identify patterns or trends (e.g., fraud detection systems). Complex Event Processing tools allow you to analyze streams of events and detect significant event sequences.

### 8. **Fault Tolerance and Resilience:**
   - Because components in EDA are decoupled, individual failures can often be isolated, making the system more resilient. If a consumer fails, the event is still persisted in the event stream and can be processed once the consumer recovers.

### 9. **Event-Driven Systems in Microservices:**
   - In microservice architectures, EDA helps in communication between services. Instead of relying on synchronous REST calls, services publish events to a central event bus, and other services subscribe to the events they care about. This reduces the tight dependencies between services.

### 10. **Event Types:**
   - **Event Notification**: Consumers are notified of an event, but the event data itself may not be fully included. The consumer may need to retrieve additional information.
   - **Event-Carried State Transfer**: The event itself carries all the necessary information for the consumer to process it. This pattern helps eliminate the need for subsequent API calls to retrieve additional data.
   - **Event Sourcing**: This design pattern uses events as the primary source of truth, recording state changes as a series of events, which allows you to reconstruct the system’s state at any point.

### 11. **Challenges:**
   - **Event Ordering**: Ensuring that events are processed in the correct order can be complex, especially in distributed systems.
   - **Idempotency**: Events can be processed multiple times, so systems must ensure that they handle events in an idempotent way (i.e., processing an event multiple times doesn’t change the result).
   - **Debugging and Monitoring**: Because of the asynchronous nature of EDA, it can be harder to trace issues or monitor the flow of events, which often requires specialized monitoring tools.

### Use Cases:
- **Microservices**: Decoupling services that need to communicate asynchronously.
- **IoT systems**: Processing streams of sensor data.
- **Real-Time Analytics**: Systems that react to real-time events, such as fraud detection or financial trading.
- **User Activity Tracking**: Tracking user behavior in real-time on websites or mobile apps.

In summary, Event-Driven Architecture enables scalable, loosely coupled, and real-time systems where events drive the flow of operations. It's especially valuable in distributed systems, microservices, and applications requiring rapid response to changing data or external events.

## Idenpotency

Idempotency is an important concept in event-driven architectures and distributed systems where the same event might be processed multiple times. To tackle idempotency effectively, you need to ensure that processing the same event multiple times doesn’t result in inconsistent state or unintended side effects (e.g., charging a customer twice). Here are several strategies to address idempotency:

### 1. **Unique Event Identifiers**
   - Assign a unique identifier (e.g., a UUID) to each event or request. Consumers can store the processed event IDs and check them before processing an event to ensure the same event is not processed twice.
   - **Implementation example**:
     - When an event arrives, the system checks if the event ID has already been processed (usually stored in a database or a cache).
     - If the event ID exists, it is ignored.
     - If the event ID does not exist, the event is processed and the ID is recorded in the database.

### 2. **Idempotent Operations**
   - Make the operations performed by your system idempotent at the core. An idempotent operation means that no matter how many times it is executed, the result will be the same.
     - **Example**: If you are updating a user’s address in a database, ensure that performing the same update twice results in the same state (the address being updated once).
   - **Examples of idempotent operations**:
     - **PUT** requests in REST APIs (updating a resource).
     - **Database UPSERT** (update if exists, insert if not).
     - Setting a value to a specific state (rather than incrementing or modifying a value).

### 3. **At-Least-Once Delivery and Event De-Duplication**
   - In distributed systems, messaging systems like Kafka, RabbitMQ, or SQS may deliver the same message more than once due to network issues or retries. You can tackle this by implementing a **de-duplication** mechanism on the consumer side.
     - Store a de-duplication key (usually the event’s unique identifier) in a database or cache and reject subsequent processing if the key has already been handled.

### 4. **Database Transactions (ACID)**
   - Use database transactions to ensure that an operation either completes fully or not at all. This can prevent partial processing if an event is accidentally retried.
   - By ensuring that operations are atomic, you can avoid cases where partial changes occur (e.g., an order is half-completed).

### 5. **Locking Mechanisms**
   - If your system processes multiple events concurrently, you can use distributed locking mechanisms to ensure that only one instance of a process is allowed to modify a resource at a time.
   - For example, when a payment event arrives, you acquire a lock on the transaction ID and process it. Once processed, you release the lock. If the same event arrives again, it won’t be able to acquire the lock.

### 6. **Event Versioning**
   - Use version numbers for state changes or events. Each time an entity’s state changes (e.g., a user’s account balance), it is assigned a version number. The system can then compare the event’s version number with the current version in the system to determine whether to process the event or skip it.
   - This is particularly useful for **event sourcing** scenarios, where the state of an entity is rebuilt by replaying events.

### 7. **Delayed Event Processing**
   - In cases where it is difficult to immediately determine if an event has been duplicated, consider delaying the processing of the event for a short period (e.g., a few seconds). In that time, duplicate events may arrive and can be handled before the original one is processed.

### 8. **Stateless Processing**
   - Where possible, design your systems to be stateless for particular operations. Stateless services rely purely on the input they receive (e.g., event data) and are less prone to idempotency issues because they don’t store internal state that can be affected by repeated events.

### 9. **Compensation or Rollback Mechanisms**
   - In cases where it’s impossible to prevent non-idempotent side effects (e.g., charging a customer’s credit card), implement compensation mechanisms to undo unintended actions. For example, if a customer is charged twice, your system could trigger an automatic refund.
   - **Saga pattern**: A distributed transaction pattern where each service involved in a transaction has compensating actions to undo its changes in case of failure.

### 10. **Use an Idempotency Key in APIs**
   - For APIs, you can require clients to send an **idempotency key** with each request. This key allows the server to detect and discard duplicate requests based on the same key.
     - This is commonly used in payment gateways (e.g., Stripe), where a unique idempotency key is sent with each payment request. If the same request is sent again with the same key, the server will return the result of the original request instead of processing it again.

#### Implementation of Idempotency Key Handling

**Client-side key generation**

- Use unique ID on client side
- use common algorithms like UUID, Snowflake ID etc.
- client must generate ID and store it in session and cookies
    - cookies in case the session context is lost in browser
- client must react on error message 409 Conflict that 
- also client must clear idempotency key after successful completion of process

```
HTTP/1.1 409 Conflict
Content-Type: application/json

{
  "error": "Request already in progress",
  "message": "Your request with idempotency key 'abc-123' is currently being processed."
}

```

- API-Gateway can check if key already exists (Cache or Bloom-Filter) and reject if its already existing
    - by that the backend services only gets requests that are relevant