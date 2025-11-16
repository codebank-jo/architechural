# Software Architectural Styles

A cleaned, consistent reference for common architectural styles. Each style includes: definition, when to choose it, pros / cons, simple diagram, and quick notes on operational/structural implications.

---

## Monolithic

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

## Layered (N‑Tier)

**Definition**  
Organized into layers (Presentation → Business → Data). Each layer has clear responsibilities.

**When to choose**  
Enterprise apps needing separation of concerns and clear team responsibilities.

**Pros / Cons**

| Pros | Cons |
|---|---|
| Clear structure and separation of concerns | Can become rigid and add latency between layers |
| Easier to reason about responsibilities | Over‑layering leads to unnecessary complexity |

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

## Client‑Server

**Definition**  
Clients request services from centralized servers (classic request/response).

**When to choose**  
Simple distributed systems or systems with clear client/server roles.

**Pros / Cons**

| Pros | Cons |
|---|---|
| Centralized control, easy to secure | Server can become bottleneck |
| Simple communication model | Scaling servers requires careful design |

**Diagram**
```text
Client --> Load Balancer --> Server --> Database
```

**Notes**  
- Add load balancers, caching, and horizontal scaling to improve capacity.

---

## Microservices

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

## Event‑Driven

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

## Microkernel (Plug‑in)

**Definition**  
Core system with extension points (plug‑ins) that add functionality.

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

## Space‑Based

**Definition**  
Uses distributed in-memory data grids and partitioning to avoid central bottlenecks.

**When to choose**  
High-throughput, low-latency systems needing horizontal scale with in-memory state.

**Pros / Cons**

| Pros | Cons |
|---|---|
| Excellent horizontal scalability and concurrency | Complex consistency and state management |
| Avoids single database bottleneck | Operational and debugging complexity |

**Diagram**
```text
[Node A] <--> [Distributed Data Grid] <--> [Node B]
                      ^
                      |
                   [Node C]
```

**Notes**  
- Good for session stores, in-memory processing, and real-time systems.  
- Ensure robust partitioning and replication strategies.

---

## SOA (Service‑Oriented Architecture)

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

## Quick comparison (one‑line)

| Style | Best for | Caution |
|---|---:|---|
| Monolith | Fast iteration | Watch coupling |
| Layered | Clear separation | Avoid excess layers |
| Client‑Server | Simple distributed apps | Scale server properly |
| Microservices | Large, autonomous teams | Invest in ops & contracts |
| Event‑Driven | Asynchronous, decoupled flows | Manage consistency & tracing |
| Microkernel | Extensible platforms | Govern plugin lifecycle |
| Space‑Based | High throughput stateful apps | Complex state management |
| SOA | Enterprise integration | Avoid ESB bottlenecks |

---

## Practical tips

- Document assumptions and constraints before choosing a style.  
- Consider hybrid approaches (e.g., monolithic modular core + microservices for unstable domains).  
- Prioritize operational readiness: automated CI/CD, observability, and recovery runbooks.  
- Evolve architecture incrementally; measure with metrics (lead time, MTTR, error rate).
