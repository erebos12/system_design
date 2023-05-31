# WebSockets

## What is it?
- duplex protocol (2-way-protocol)
- build on top of TCP
- persistent connection
- mostly needed when your server needs to send messages actively


## Pros
- Connection is established only once (TCP connection expensive)
- real time message delivery to client i.e. instant messaging service
- server can push message, so no polling from client needed

## Cons
- more complicated to implement than HTTP, mostly stateful
- load balancer can have trouble since long term connection is used
- new "protocol" needs to be re-invented (unlike in REST)