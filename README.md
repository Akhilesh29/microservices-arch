# Microservices Architecture Example

This project demonstrates a basic microservices architecture using Java Spring Boot. The architecture follows best practices for microservices design and includes proper service isolation, API Gateway pattern, and service discovery.

## Architecture Overview

```mermaid
graph TD
    Client[Client] --> |HTTP/HTTPS| Gateway[API Gateway]
    Gateway --> |Auth Request| Auth[Authentication Service]
    Gateway --> |Product Request| Product[Product Service]
    Gateway --> |Order Request| Order[Order Service]
    Gateway --> |User Request| User[User Service]
    
    Auth --> |JWT| Gateway
    Product --> |Data| Gateway
    Order --> |Data| Gateway
    User --> |Data| Gateway
    
    Product --> |Store Data| ProductDB[(Product DB)]
    Order --> |Store Data| OrderDB[(Order DB)]
    User --> |Store Data| UserDB[(User DB)]
    Auth --> |Store Data| AuthDB[(Auth DB)]
```



## Communication Flow

```mermaid
sequenceDiagram
    participant Client
    participant Gateway
    participant Auth
    participant Service
    
    Client->>Gateway: Request
    Gateway->>Auth: Validate Token
    Auth-->>Gateway: Token Valid
    Gateway->>Service: Forward Request
    Service-->>Gateway: Response
    Gateway-->>Client: Response
```

## Data Flow

```mermaid
graph LR
    Client[Client] --> Gateway[API Gateway]
    Gateway --> Services[Microservices]
    Services --> DB[(Databases)]
    Services --> MQ[Message Queue]
    MQ --> Services
``` 

