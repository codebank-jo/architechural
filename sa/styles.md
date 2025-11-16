# Software Architectural Styles

A cleaned, consistent reference for common architectural styles. Each style includes: definition, when to choose it, pros / cons, simple diagram, and quick notes on operational/structural implications.

---

## Categorization of Architectural Styles

| Category | Styles | Focus |
|---|---|---|
| **Domain** | Monolithic, Microservices, Microkernel | How the system is divided and organized around business domains |
| **Communication** | Event-Driven, SOA, Pipe-and-Filter | How components exchange information and coordinate |
| **Deployment** | Layered (N-Tier), Client-Server, Space-Based | How the system is physically distributed and deployed |
| **Structure** | Hexagonal (Clean), Layered | How components are organized internally |
| **Data-Centric** | Pipe-and-Filter, Event-Driven, Space-Based | How data flows and is processed through the system |

---

## Domain-Organized Styles

Focused on how the system is divided and organized around business domains and responsibilities.

### Monolithic

**Definition**  
Single deployable unit containing presentation, business logic, and data access.

**When to choose**  
Small apps, early-stage products, teams that value simplicity and fast iteration.

**Pros / Cons**

| Pros | Cons |
|---|---|
| Simple local development and deployment | Hard to scale along independent dimensions |
| Easy to test end-to-end | Releases affect the whole system |
| Low operational overhead initially | Risk of increasing complexity and long-term coupling |

**Diagram**
```text
┌────────────────────────────────────────────────┐
│  UI  │  Business Logic  │  Data Access         │
└────────────────────────────────────────────────┘
```

**Notes**  
- Migration path: modularize, then split into services.  
- Watch for coupling and slow deployment pipelines.

---

### Microservices

**Definition**  
Application decomposed into small, independently deployable services, each owning its data and API.

**When to choose**  
Large, complex domains where independent scaling, deployment, and ownership matter.

**Pros / Cons**

| Pros | Cons |
|---|---|
| Independent deployment and scaling | Operational complexity (service discovery, observability) |
| Teams own services end-to-end | Distributed transactions and data integrity challenges |

**Diagram**
```text
[Auth]   [Catalog]   [Order]   [Payment]
   \         |          |         /
    \        |          |        /
     ---->  API Gateway / Message Bus  ---->
```

**Notes**  
- Require strong automation: CI/CD, telemetry, service mesh or API gateway.  
- Prefer domain-driven design and clear bounded contexts.

---

### Microkernel (Plug-in)

**Definition**  
Core system with extension points (plug-ins) that add functionality.

**When to choose**  
Platforms or products that need extensibility (IDEs, payment platforms).

**Pros / Cons**

| Pros | Cons |
|---|---|
| Flexible and extensible | Plugin management and compatibility can be complex |
| Keeps core small and stable | Versioning and lifecycle of plugins require governance |

**Diagram**
```text
      ┌──────────┐
      │  Kernel  │
      └──────────┘
       /   |    \
[PluginA] [PluginB] [PluginC]
```

**Notes**  
- Define clear plugin APIs and lifecycle hooks.  
- Consider sandboxing and dependency isolation.

---

## Communication-Oriented Styles

Focused on how components exchange information and coordinate with each other.

### Event-Driven

**Definition**  
Components communicate asynchronously by emitting and consuming events via an event bus.

**When to choose**  
Systems needing loose coupling, high scalability, and asynchronous workflows.

**Pros / Cons**

| Pros | Cons |
|---|---|
| Highly decoupled and scalable | Harder to reason about end-to-end flow and debugging |
| Natural fit for integration and CQRS | Eventual consistency complexities |

**Diagram**
```text
Producer --> Event Bus --> Consumer A
                             --> Consumer B
```

**Notes**  
- Pay attention to idempotency, ordering, and replay semantics.  
- Use tracing and event schemas (Avro/JSON Schema) to manage evolution.

---

### SOA (Service-Oriented Architecture)

**Definition**  
Services expose contracts and are often orchestrated via enterprise middleware (ESB).

**When to choose**  
Large organizations requiring interoperability across heterogeneous systems.

**Pros / Cons**

| Pros | Cons |
|---|---|
| Promotes reuse and interoperability | ESB can introduce coupling and operational overhead |
| Standardized contracts across teams | Can become centralized and slow to evolve |

**Diagram**
```text
Service A <--> ESB <--> Service B <--> Service C
```

**Notes**  
- Favor lightweight APIs and bounded contexts; avoid over-centralizing integration logic.

---

## Deployment-Oriented Styles

Focused on how the system is physically distributed and deployed across machines/nodes.

### Layered (N-Tier)

**Definition**  
Organized into layers (Presentation → Business → Data). Each layer has clear responsibilities.

**When to choose**  
Enterprise apps needing separation of concerns and clear team responsibilities.

**Pros / Cons**

| Pros | Cons |
|---|---|
| Clear structure and separation of concerns | Can become rigid and add latency between layers |
| Easier to reason about responsibilities | Over-layering leads to unnecessary complexity |

**Diagram**
```text
Presentation
    ↓
Business Logic
    ↓
Data Access
    ↓
Database
```

**Notes**  
- Useful as an initial architecture inside services.  
- Combine with caching and async patterns to reduce layer coupling.

---

#### Closed Layered Architecture

**Definition**  
A request must pass through each layer sequentially; a layer can only call the layer directly below it.

**When to choose**  
Systems requiring strict separation, clear boundaries, and controlled access patterns.

**Pros / Cons**

| Pros | Cons |
|---|---|
| Strict isolation between layers | Performance overhead (request passes through all layers) |
| Clear contracts and boundaries | Less flexibility; harder to optimize |
| Easier to enforce standards | Can lead to unnecessary intermediaries |

**Diagram**
```text
Presentation Layer
    ↓ (must call)
Business Logic Layer
    ↓ (must call)
Data Access Layer
    ↓ (must call)
Database
```

**Notes**  
- Each layer only knows about the layer below it.  
- Use when security, compliance, or strict governance is critical.  
- Common in legacy enterprise systems.

---

#### Open Layered Architecture

**Definition**  
Layers can bypass intermediate layers and call any layer below them directly (e.g., Presentation can call Data Access).

**When to choose**  
Systems where performance optimization and flexibility are priorities over strict layering.

**Pros / Cons**

| Pros | Cons |
|---|---|
| Better performance (skip unnecessary layers) | Risk of breaking encapsulation and creating coupling |
| More flexibility for optimization | Harder to maintain layer boundaries |
| Natural for caching and cross-layer concerns | Can become chaotic without discipline |

**Diagram**
```text
Presentation Layer
    ↓ (can call any layer below)
    ├─→ Business Logic Layer
    │       ↓ (can call any layer below)
    │       └─→ Data Access Layer
    │               ↓
    │           Database
    └────────────────────→ (bypass for caching, etc.)
```

**Notes**  
- Use for performance-critical paths.  
- Requires strong architectural governance to prevent chaos.  
- Common in modern web applications with shared caching layers.  
- Consider using adapters or facades to manage cross-layer calls.

---

## Structure-Oriented Styles

Focused on how components are organized and structured internally.

### Hexagonal (Clean Architecture)

**Definition**  
Isolates business logic in the center (core domain) with adapters at the boundaries to interact with external systems (UI, databases, APIs).

**When to choose**  
Systems where business logic must remain independent of external frameworks and technologies.

**Pros / Cons**

| Pros | Cons |
|---|---|
| Business logic is framework-agnostic and testable | Additional layer of indirection and complexity |
| Easy to swap implementations (ports & adapters) | Overkill for simple CRUD applications |
| Clear separation between core and external concerns | Requires discipline to maintain boundaries |

**Diagram**
```text
        UI Layer (Adapters)
           /    |    \
         REST  gRPC  GraphQL
           \    |    /
         [Application Layer]
           /    |    \
       [Business Logic Core]
           /    |    \
         DB   Cache  Messages
        (Adapters)
```

**Notes**  
- Core domain has no knowledge of external systems (databases, web frameworks).  
- Use dependency injection to wire adapters.  
- Ports define contracts; adapters implement them.  
- Excellent for domain-driven design (DDD) and microservices.

---

## Data-Centric Styles

Focused on how data flows and is processed through the system.

### Pipe-and-Filter

**Definition**  
Data flows through a sequence of independent filters (processors) connected by pipes. Each filter transforms data and passes it to the next.

**When to choose**  
Data processing pipelines, ETL systems, stream processing, and batch workflows.

**Pros / Cons**

| Pros | Cons |
|---|---|
| Highly composable and reusable filters | Debugging data flow can be complex |
| Easy to parallelize and distribute | Latency overhead from chaining |
| Clear separation of concerns | Error handling and backpressure management needed |

**Diagram**
```text
Input --> [Filter A] --> [Filter B] --> [Filter C] --> Output
              |              |              |
            Data           Data           Data
```

**Notes**  
- Each filter is stateless and independent; enables parallel processing.  
- Use with stream processing frameworks (Kafka, Spark, Flink) for scalability.  
- Define clear data contracts between filters.

---

## Quick Comparison

| Style | Category | Best for | Caution |
|---|---|---|---|
| Monolith | Domain | Fast iteration | Watch coupling |
| Microservices | Domain | Large, autonomous teams | Invest in ops & contracts |
| Microkernel | Domain | Extensible platforms | Govern plugin lifecycle |
| Event-Driven | Communication | Asynchronous, decoupled flows | Manage consistency & tracing |
| SOA | Communication | Enterprise integration | Avoid ESB bottlenecks |
| Layered | Deployment | Clear separation | Avoid excess layers |
| Client-Server | Deployment | Simple distributed apps | Scale server properly |
| Space-Based | Deployment | High throughput stateful apps | Complex state management |
| Hexagonal | Structure | Business logic isolation | Avoid over-engineering |
| Pipe-and-Filter | Data-Centric | Data processing pipelines | Debug end-to-end flow |

---

## Practical Tips

- Document assumptions and constraints before choosing a style.  
- Consider hybrid approaches (e.g., monolithic modular core + microservices for unstable domains).  
- Prioritize operational readiness: automated CI/CD, observability, and recovery runbooks.  
- Evolve architecture incrementally; measure with metrics (lead time, MTTR, error rate).
