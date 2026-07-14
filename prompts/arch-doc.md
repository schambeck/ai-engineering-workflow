You are a senior software architect specializing in Java, Spring Boot, Angular, PrimeNG, Clean Architecture, DDD, and multi-tenant SaaS systems.

I want you to create a **single HTML page** to visually document the workflows between packages, layers, and components of the **Fleet Control** system.

The page should let me click on a system action, such as:

- Vehicle registration
- Driver registration
- Trip scheduling
- Trip start
- Trip completion
- Trip cancellation
- Creation of a preventive maintenance plan
- Automatic maintenance generation
- Execution of preventive maintenance
- Corrective maintenance recording
- Document upload
- Tire control
- Report generation
- Automatic notification
- Real-time monitoring
- Integration via external API
- Event via WebSocket
- Blocking due to expired subscription

When clicking an action, the page should:

1. Visually highlight the packages/components involved in the flow.
2. Draw or highlight the connections between components.
3. Show the execution order.
4. Explain what is passed from one package to another.
5. Show the DTOs, commands, entities, events, and responses involved.
6. Display the business rules applied at each step.
7. Display possible exceptions.
8. Display triggered domain or WebSocket events.
9. Display impacted metrics.
10. Display suggested endpoints.

The page should be driven by a JSON object embedded in the HTML itself.

---

# Expected architecture

Consider an architecture based on layers and packages like this:

```text
com.controlefrotas
├── application
│   ├── usecase
│   ├── command
│   ├── query
│   ├── service
│   └── dto
│
├── domain
│   ├── model
│   ├── event
│   ├── exception
│   ├── repository
│   ├── service
│   └── valueobject
│
├── infrastructure
│   ├── persistence
│   │   ├── entity
│   │   ├── mapper
│   │   └── repository
│   ├── messaging
│   ├── security
│   ├── tenant
│   ├── websocket
│   ├── notification
│   └── integration
│
├── presentation
│   ├── rest
│   ├── request
│   ├── response
│   └── exceptionhandler
│
└── frontend
    ├── angular
    ├── components
    ├── pages
    ├── services
    ├── guards
    └── interceptors
````

---

# Mandatory components on screen

The HTML page must show all these components as visual blocks:

## Frontend

* Angular Page
* PrimeNG Form
* PrimeNG Table
* Angular Service
* HTTP Interceptor
* Auth Guard
* WebSocket Client

## Presentation Layer

* REST Controller
* Request DTO
* Response DTO
* Exception Handler

## Application Layer

* Use Case
* Command
* Query
* Application Service
* Transaction Boundary

## Domain Layer

* Aggregate Root
* Entity
* Value Object
* Domain Service
* Domain Event
* Business Rule
* Domain Exception
* Repository Interface

## Infrastructure Layer

* JPA Entity
* JPA Repository
* Mapper
* PostgreSQL
* Liquibase
* Keycloak Security
* Tenant Resolver
* Notification Adapter
* WebSocket Publisher
* External API Adapter
* Mercado Pago Adapter

## Observability

* Logger
* Metrics
* Audit Log

---

# Mandatory flows

Document at least these flows in the JSON and in the interface:

## 1. Vehicle registration

Expected flow:

```text
Angular Page
→ PrimeNG Form
→ Angular Service
→ HTTP Interceptor
→ REST Controller
→ Request DTO
→ Use Case
→ Command
→ Aggregate Root Vehicle
→ Business Rules
→ Repository Interface
→ Mapper
→ JPA Entity
→ JPA Repository
→ PostgreSQL
→ Domain Event
→ Audit Log
→ Response DTO
→ Angular Page
```

Explain that data such as plate, model, year, fuel type, Renavam, chassis, engine, and acquisition mileage are passed.

Include rules:

* Plate is mandatory.
* Plate cannot be duplicated within the tenant.
* Acquisition mileage cannot be negative.
* Vehicle starts with operational status `PARADO`.

---

## 2. Driver registration

Include data:

* Name
* CPF
* CNH (driver's license)
* CNH category
* CNH expiration date
* Active/inactive status

Rules:

* CPF is mandatory.
* CNH is mandatory.
* Expired CNH blocks use in trips.
* Driver starts as `ATIVO` and operationally `PARADO`.

---

## 3. Trip scheduling

Flow:

```text
Angular Page
→ PrimeNG Form
→ Angular Service
→ REST Controller
→ ScheduleTripUseCase
→ Trip Aggregate
→ Vehicle Repository
→ Driver Repository
→ Business Rules
→ PostgreSQL
→ TripScheduledEvent
→ Notification Adapter
→ Response DTO
```

Rules:

* Vehicle must be available.
* Driver must be active.
* Driver must have a valid CNH.
* Vehicle cannot be on another trip.
* Driver cannot be on another trip.
* Trip is created with status `PROGRAMADA`.

---

## 4. Trip start

Rules:

* Trip must be `PROGRAMADA`.
* Starting mileage must be provided.
* Vehicle changes to `EM_TRANSITO`.
* Driver changes to `EM_TRANSITO`.
* Trip changes to `EM_TRANSITO`.
* Event `TripStartedEvent` must be fired.
* WebSocket must publish an update to the dashboard.

---

## 5. Trip completion

Rules:

* Trip must be `EM_TRANSITO`.
* Ending mileage must be greater than starting mileage.
* Trip changes to `FINALIZADA`.
* Vehicle returns to `PARADO`.
* Driver returns to `PARADO`.
* Metrics are recalculated.
* Maintenance plan is checked.
* May generate preventive maintenance.
* Events `TripFinishedEvent`, `VehicleMileageUpdatedEvent`, and `MaintenanceDueDetectedEvent`.

---

## 6. Trip cancellation

Rules:

* Trip can only be cancelled if it has not yet been completed.
* Cancelled trip does not change metrics.
* Cancelled trip does not change the vehicle's mileage.
* Event `TripCancelledEvent`.

---

## 7. Creation of a preventive maintenance plan

Rules:

* Vehicle must exist.
* Frequency can be by mileage, time, or both.
* Plan generates future schedules.
* Event `MaintenancePlanCreatedEvent`.

---

## 8. Automatic preventive maintenance generation

Rules:

* System checks current mileage and time since the last maintenance.
* If the limit is reached, generates a pending maintenance.
* Sends a notification.
* Event `PreventiveMaintenanceGeneratedEvent`.

---

## 9. Execution of preventive maintenance

Rules:

* Maintenance must be pending.
* Cannot be executed twice.
* Updates history.
* Reschedules the next maintenance.
* May change the vehicle to available.
* Event `MaintenanceExecutedEvent`.

---

## 10. Corrective maintenance recording

Rules:

* Created manually.
* Does not interfere with the preventive plan.
* Records cost, supplier, mileage, and description.
* Event `CorrectiveMaintenanceRegisteredEvent`.

---

## 11. Document management

Flow for uploading CRLV, insurance, contracts, invoices, and technical reports.

Rules:

* Document belongs to a tenant.
* Document may have an expiration date.
* Expired document generates a notification.
* Re-upload generates a new version.

---

## 12. Tire control

Flows:

* Tire registration
* Rotation
* Replacement
* Wear alert

Rules:

* Tire has serial number, manufacturer, model, DOT, size, and position.
* Rotation changes position.
* Replacement records the reason.
* Service life can be controlled by mileage or time.

---

## 13. Reports and exports

Flows:

* Trip report
* Fuel consumption report
* Maintenance report
* Driver report
* PDF export
* Excel export
* CSV export

---

## 14. Automatic notifications

Types:

* Expired CNH
* Overdue maintenance
* Expired document
* Expired subscription
* Route delay
* Performance anomaly

---

## 15. Real-time monitoring

Include:

* WebSocket Client
* WebSocket Publisher
* Dashboard
* VehicleLocationUpdatedEvent
* Route/trajectory replay

---

## 16. Subscription and payment

Include:

* Mercado Pago Adapter
* Subscription Use Case
* HTTP 402 Payment Required
* Blocking of paid modules
* Subscription reauthorization

---

# Mandatory JSON structure

Include a JavaScript object called `architectureDocumentation` in the HTML.

It should follow this structure:

```json
{
  "system": {
    "name": "Fleet Control",
    "description": "Multi-tenant SaaS system for managing vehicles, drivers, trips, maintenance, documents, tires, reports, and real-time monitoring.",
    "architectureStyle": "Clean Architecture + DDD + Layered Architecture",
    "backendStack": ["Java", "Spring Boot", "PostgreSQL", "Liquibase", "Keycloak"],
    "frontendStack": ["Angular", "PrimeNG"],
    "integrationStack": ["REST API", "WebSocket", "STOMP", "Mercado Pago"]
  },
  "packages": [
    {
      "id": "frontend-angular-page",
      "name": "Angular Page",
      "layer": "Frontend",
      "description": "Screen responsible for orchestrating user interaction."
    }
  ],
  "flows": [
    {
      "id": "vehicle-registration",
      "name": "Vehicle registration",
      "module": "Vehicles",
      "description": "Flow responsible for registering a new vehicle in the fleet.",
      "trigger": "User clicks New Vehicle and saves the form.",
      "steps": [
        {
          "order": 1,
          "componentId": "frontend-angular-page",
          "componentName": "Angular Page",
          "action": "Captures the data entered by the user.",
          "input": "PrimeNG Form",
          "output": "VehicleFormModel",
          "notes": "Contains plate, model, year, fuel type, and acquisition mileage."
        }
      ],
      "connections": [
        {
          "from": "frontend-angular-page",
          "to": "primeng-form",
          "payload": "VehicleFormModel",
          "description": "Data entered in the form."
        }
      ],
      "businessRules": [
        {
          "id": "BR-VEHICLE-001",
          "description": "License plate is mandatory."
        }
      ],
      "exceptions": [
        {
          "type": "DuplicateVehiclePlateException",
          "message": "A vehicle with this plate already exists in this tenant."
        }
      ],
      "events": [
        {
          "name": "VehicleCreatedEvent",
          "when": "After the vehicle is successfully persisted."
        }
      ],
      "endpoints": [
        {
          "method": "POST",
          "path": "/api/v1/vehicles",
          "request": "CreateVehicleRequest",
          "response": "VehicleResponse"
        }
      ],
      "metrics": [
        "vehicles_total",
        "vehicle_registration_success_total",
        "vehicle_registration_error_total"
      ]
    }
  ]
}
```

Complete this JSON with all the mandatory packages, components, and flows.

---

# Mandatory visual behavior

The page must have:

1. Header with the system name.
2. Short description of the architecture.
3. Side menu or top bar with all the flows.
4. Central area with the component/package map.
5. Side panel with details of the selected flow.
6. Collapsible JSON area at the end.
7. Button to copy the JSON.
8. Button to copy the documentation of the selected flow.
9. Button to reset the highlight.
10. Color legend by layer.

---

# Mandatory interactivity

When clicking a flow:

* Involved components must be highlighted.
* Uninvolved components must have reduced opacity.
* Flow connections must appear or be highlighted.
* The side panel must show:

  * Flow name
  * Objective
  * Trigger
  * Ordered steps
  * Payloads between components
  * Business rules
  * Exceptions
  * Events
  * Endpoints
  * Metrics
* There must be a timeline of the flow.
* There must be a list of "what is passed between packages".

---

# Visual design

Use a modern, technical, and professional design.

Suggested layer colors:

* Frontend: blue
* Presentation: purple
* Application: green
* Domain: orange
* Infrastructure: gray
* Observability: red

Use:

* Cards
* Badges
* Connection lines
* Arrows
* Timeline
* Details panel
* Compact tables
* Responsive layout

Do not use external libraries.

---

# Technical requirements

The HTML must be self-contained:

* Inline CSS
* Inline JavaScript
* Inline JSON
* No external dependencies
* No CDN
* No external images
* Must work simply by opening the `.html` file in the browser

Use only:

* HTML
* CSS
* Plain JavaScript
* Inline SVG, if necessary

---

# Code quality requirements

* Organized code.
* Small, readable JavaScript functions.
* Clear names.
* Logical separation between:

  * data
  * rendering
  * events
  * utilities
* Avoid duplication.
* Use constants.
* Use comments only when they help.
* Generate a ready-to-use HTML.

---

# Expected result

Return exclusively the complete content of the HTML file.

Do not explain anything outside the HTML.

Do not use Markdown.

Do not say "here it is".

Just generate the final complete HTML in: docs/arch-doc.md
