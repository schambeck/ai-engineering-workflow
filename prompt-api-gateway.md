# Implement API Gateway for the backend ecosystem

## Context

Create an API Gateway application to centralize access to backend services.

Projects involved initially:

- api

Desired architecture:

```pre
Client
|
v
API Gateway
|
+---- api
|
+---- future microservices
```

The Gateway will be the single entry point of the ecosystem.

---

# Technology

Use:

- Java 21
- Spring Boot 3.x
- Spring Cloud Gateway
- Maven

Follow existing standards in the backend projects.

---

# Objectives

Implement an Edge Gateway layer responsible for:

- routing
- security
- traffic control
- observability
- request standardization

---

# Before implementing

Assess:

1. Current versions of the backend projects.
2. Existing authentication patterns.
3. Endpoint structure.
4. Need for future compatibility with Kubernetes/OpenShift/AWS.

---

# Features

## 1. Routing

Create configuration for forwarding:

Example:

```pre
/api/fila/**

    |

api
```

Use external configuration:

application.yml


Example:

```yaml
spring:
 cloud:
   gateway:
     routes:
       - id: fila-service
         uri: http://api:8080
         predicates:
           - Path=/api/fila/**
```
