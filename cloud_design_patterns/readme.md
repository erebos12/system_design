# Cloud Deign Pattern

## Relevant Features for Offloading

1. Token Handling / Validation
2. Encryption
3. SSL Certificates
4. Authorization / Authentication
5. Throtteling
6. Logging & Metrics & Monitoring
7. Routing


## Gateway Offloading Pattern (Feature Offloading)

Take away responsibiltities from a single services and offload them to a a other services like gateway.
Be sure that Gateway support high-availability and scalability!

1. SSL Offloading

- Load-Balancer decrypts incoming traffic with SSL certificates
- internal traffic is unencrpyted then
- so no SSL certificate handling within the services needed

![alt text](image.png)

2. Offloading Authorization / Authentication

![alt text](image-1.png)

3. Offloading Logging & Monitoring

![alt text](image-2.png)

4. Encryption Offloading to a Vault

![alt text](image-3.png)

5. Throtteling Offloading

![alt text](image-4.png)

Final Pattern:

![alt text](image-5.png)

## Gateway Routing Pattern

Routing rules/function in one singel service such as Gateway.
Be aware that these rules DO NOT include load balancing features i.e. 
route 50% to service A and 50% to service B.

Problem

![alt text](image-6.png)

Use Gateway for routing:
![alt text](image-7.png)

In case of a new service

![alt text](image-8.png)