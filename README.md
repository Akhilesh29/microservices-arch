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
## Service Components

1. **API Gateway**
   - Entry point for all client requests
   - Handles routing and request forwarding
   - Implements rate limiting and request validation
   - Built with Spring Cloud Gateway

2. **Authentication Service**
   - Handles user authentication and authorization
   - Manages JWT tokens
   - User session management
   - Built with Spring Security

3. **Product Service**
   - Manages product catalog
   - Handles product CRUD operations
   - Product search and filtering
   - Built with Spring Data JPA

4. **Order Service**
   - Processes orders
   - Manages order status
   - Handles payment integration
   - Built with Spring Boot

5. **User Service**
   - Manages user profiles
   - Handles user preferences
   - User data management
   - Built with Spring Boot


## API Documentation

Each service includes its own Swagger documentation accessible at:
- API Gateway: `http://localhost:8080/api-docs`
- Auth Service: `http://localhost:8081/api-docs`
- Product Service: `http://localhost:8082/api-docs`
- Order Service: `http://localhost:8083/api-docs`
- User Service: `http://localhost:8084/api-docs`
