You are a specialist in UX Architecture, Product Design Systems, SaaS Enterprise, and visualization of complex architectural flows.

Create an interactive visual experience in the style of a technical dashboard for the current project.

The goal is to create a single visual and interactive page, in the style of an "Architecture Explorer," where the user can navigate the system's flows and see how components, packages, and layers interact internally.

The experience should feel like a blend of:

- interactive technical documentation
- architectural map
- flow observability
- domain explorer
- visual system design
- dependency graph
- workflow explorer

The result should be visually impressive, modern, and extremely clear.

---

# Interface objective

The page should allow the user to:

1. See the entire system architecture.
2. Navigate between the system's modules.
3. Click on specific flows.
4. See the complete path between frontend, backend, domain, and infrastructure.
5. Understand which data passes between components.
6. Understand which business rules are executed.
7. Understand which events are triggered.
8. Understand which exceptions can occur.
9. Understand which metrics are impacted.
10. Understand which external integrations participate in the flow.

---

# Stack and technical context

The system is a multi-tenant fleet management SaaS.

Architecture:

- Clean Architecture
- DDD
- Layered Architecture
- Event-Driven Architecture
- REST + WebSocket

Backend:

- Java
- Spring Boot
- PostgreSQL
- Liquibase
- Keycloak
- WebSocket/STOMP

Frontend:

- Angular
- PrimeNG

Integrations:

- Mercado Pago
- WebSocket
- External REST APIs

---

# System modules

The interface should include:

- Vehicles
- Drivers
- Trips
- Maintenance
- Documents
- Tires
- Reports
- Notifications
- Monitoring
- Subscriptions
- Integrations

---

# Required flows

The experience should allow selecting and visualizing:

1. Vehicle registration
2. Driver registration
3. Trip scheduling
4. Trip start
5. Trip completion
6. Trip cancellation
7. Preventive plan creation
8. Automatic maintenance generation
9. Preventive maintenance execution
10. Corrective maintenance recording
11. Document upload
12. Tire control
13. Report generation
14. Automatic notifications
15. Real-time monitoring
16. REST API integration
17. WebSocket events
18. Subscription management
19. Payment-related blocking
20. Subscription reauthorization

---

# Visual architectural structure

The page should visually represent the following layers:

## Frontend

- Angular Pages
- PrimeNG Components
- Angular Services
- HTTP Interceptors
- Route Guards
- WebSocket Client

## Presentation Layer

- REST Controllers
- Request DTOs
- Response DTOs
- Exception Handlers

## Application Layer

- Use Cases
- Commands
- Queries
- Application Services
- Transaction Boundary

## Domain Layer

- Aggregates
- Entities
- Value Objects
- Domain Services
- Business Rules
- Domain Events
- Domain Exceptions
- Repository Interfaces

## Infrastructure Layer

- JPA Entities
- JPA Repositories
- PostgreSQL
- Liquibase
- Keycloak
- Tenant Resolver
- Notification Adapter
- WebSocket Publisher
- Mercado Pago Adapter
- External API Adapter

## Observability

- Logger
- Metrics
- Audit Log

---

# Required interactivity

When the user clicks on a flow:

- Highlight only the components involved
- Reduce the opacity of the others
- Animate the flow path
- Show arrows between components
- Show payloads between layers
- Show commands and DTOs
- Show business rules executed
- Show events emitted
- Show possible exceptions
- Show REST endpoints involved
- Show WebSocket events
- Show impacted metrics
- Show logs/audit records generated

---

# Visual experience

Create a premium, modern design.

Visual references:

- observability dashboards
- architecture maps
- dependency graphs
- system explorer
- infrastructure topology
- modern developer portals

Style:

- elegant dark mode
- light glassmorphism
- soft borders
- subtle glow
- technical grid
- enterprise look
- highly interactive visuals

---

# Required layout

## Topbar

Containing:

- system name
- architecture description
- flow search
- filter by module
- filter by layer

---

## Sidebar

List of:

- modules
- flows
- categories

---

## Central area

Visual architectural map.

The layers should be organized horizontally:

Frontend
→ Presentation
→ Application
→ Domain
→ Infrastructure
→ Observability

Each layer should have its components.

Connections should be drawn visually.

---

## Right side panel

When a flow is selected:

Show:

- flow name
- objective
- trigger
- timeline
- full sequence
- payloads
- rules
- events
- exceptions
- endpoints
- metrics
- observability
- integrations

---

# Flow visualization

Example:

Vehicle registration

Angular Page
→ PrimeNG Form
→ Angular Service
→ HTTP Interceptor
→ REST Controller
→ Request DTO
→ CreateVehicleUseCase
→ CreateVehicleCommand
→ Vehicle Aggregate
→ Business Rules
→ Repository Interface
→ VehicleJpaEntity
→ VehicleJpaRepository
→ PostgreSQL
→ VehicleCreatedEvent
→ Audit Log
→ Metrics
→ Response DTO
→ Angular UI Update

Show:

- what goes in
- what comes out
- payload
- rule applied
- status changed
- event triggered

---

# Important business rules

Visually include rules such as:

## Vehicles

- License plate required
- License plate unique per tenant
- Acquisition mileage >= 0
- Vehicle starts as STOPPED

## Drivers

- Driver's license required
- Driver's license valid
- Cannot be on two trips at once

## Trips

- Vehicle available
- Driver active
- Trip SCHEDULED
- Final mileage > initial mileage

## Maintenance

- Preventive vs corrective
- Do not execute twice
- Automatic rescheduling

## Subscriptions

- HTTP 402 Payment Required
- Module blocking
- Reauthorization

---

# Required JSON

The entire interface must be driven by a JavaScript object called:

```js
const architectureDocumentation = { ... }
````

This JSON must contain:

* system
* layers
* packages
* components
* flows
* businessRules
* events
* exceptions
* endpoints
* metrics
* integrations
* websocketTopics
* observability

Components and connections should be rendered dynamically from the JSON.

---

# Extra features

Add:

* zoom
* pan
* architectural minimap
* animated highlight
* text search
* filters
* "copy flow" button
* "export JSON" button
* "reset flow" button
* legend by layer
* visual timeline
* flow breadcrumb

---

# Technical requirements

The experience must be generated as a single page.

Everything must be self-contained:

* no backend
* no APIs
* no CDN
* no external dependencies

Use only:

* HTML
* CSS
* Plain JavaScript
* Inline SVG

---

# Quality requirements

* Extremely organized code
* Visual componentization
* Small JavaScript functions
* Data separated from rendering
* Easy maintenance
* Scalable structure
* Professional visuals
* Excellent UX
* Good performance

---

# Expected result

Generate an interactive visual experience of enterprise architecture.

The interface should look like a professional architectural exploration tool used by senior engineers, architects, and platform teams.

Return only the complete content of the page.

Do not explain anything outside of the interface.

```

Adapted from the original attached prompt. :contentReference[oaicite:0]{index=0}
```

Generate the final result at: docs/dashboard-architecture-explorer.html
