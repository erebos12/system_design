## What protocol to use ?

1. Do you have an external API ? 
   - gRPC not supported by browser and harder to implement
   - REST, WebSocket, GraphQL, UDP, Long Polling can be an option
2. Is communication bi-directional (server needs to push messages) ?
   - prefer WebSockets or UDP
3. High throughput needed ?
   - prefer WebSockets, gRPC or UDP
4. Support for WebBrowser ?
   - No gRPC !
   - REST, GraphQL, WebSockets or Long Polling