# Introduction to Software Architecture

> Overview  
> Software architecture is the high-level structure of a system: its components, responsibilities, and interactions.  
> It guides design decisions to meet business goals such as scalability, reliability, and maintainability.

## Table of contents
- [Definition & Purpose](#definition--purpose)  
- [Key Aspects](#key-aspects)  
- [Core Components](#core-components)  
- [Infrastructure & Deployment](#infrastructure--deployment)  
- [Characteristics of Good Architecture](#characteristics-of-good-architecture)  
  - [Operational](#operational)  
  - [Structural](#structural)  
  - [Cross‑Cutting](#cross‑cutting)  
- [Summary](#summary)

---

## Definition & Purpose

**Definition:** The high-level organization of a software system, describing components, interfaces, and interactions.

**Purpose:** Provide a blueprint that ensures the system is scalable, maintainable, performant, secure, and aligned with business requirements.

**Analogy:** Like building architects design rooms, plumbing, and wiring, software architects design modules, APIs, and data flows.

---

## Key Aspects

| # | Aspect | Explanation |
|---:|--------|-------------|
| 1 | High-Level Structure | Defines overall system structure (not implementation details) |
| 2 | Blueprint for Development | Guides developers similar to building blueprints |
| 3 | Component Organization | How modules/services/layers are arranged and interact |
| 4 | Communication Mechanisms | APIs, message queues, protocols for component interaction |
| 5 | Technology Decisions | Frameworks, databases, platforms, tools selection |
| 6 | Non-Functional Qualities | Scalability, performance, security, reliability, maintainability |
| 7 | Business Alignment | Maps technical design to business needs and requirements |
| 8 | Evolution Roadmap | Foundation for future growth, upgrades, and integration |
| 9 | Cross-Cutting Concerns | Logging, monitoring, auth, error handling applied system-wide |
|10 | Documentation Tool | Shared language for developers, managers, and stakeholders |

---

## Core Components

- Components / Modules / Services — encapsulate functionality with defined interfaces.  
- Connectors — communication paths between components (HTTP, gRPC, message brokers).  
- Data — storage systems and data flow (databases, caches, event stores).  
- Interfaces — entry points for users or external systems (REST endpoints, GUIs).

Example: A mobile UI calls backend services via REST:

```http
GET /api/v1/products HTTP/1.1
Host: api.example.com
Authorization: Bearer <token>
```

---

## Infrastructure & Deployment

- Deployment targets: servers, cloud platforms, containers, orchestration (e.g., Kubernetes).  
- Runtime concerns: scaling, networking, secrets management, observability.

Example: Microservices deployed in containers on Kubernetes with an ingress controller, autoscaling, and centralized logging.

---

## Characteristics of Good Architecture

Operational — runtime qualities that determine how the system runs in production (performance, scalability, availability, fault tolerance, observability).  
Example keywords: Run | Serve | Recover — (latency, autoscaling, circuit breakers, monitoring).

Structural — organization and maintainability of the code and components (modularity, boundaries, testability, data strategy).  
Example keywords: Build | Organize | Isolate — (microservices, bounded contexts, contract tests).

Cross‑Cutting — system-wide concerns that apply across components (logging, config & secrets, CI/CD, security, policy).  
Example keywords: Everywhere | Policies | Glue — (centralized logging, Vault, automated pipelines).

---

### Operational

| Characteristic | Description | Example | Metrics / Notes |
|---|---|---|---|
| Performance | How fast requests are handled | P95 latency < 100ms for interactive endpoints | Latency, throughput, P95/P99 |
| Scalability | Ability to handle growth (users / data) | Horizontal autoscaling based on queue depth | Max QPS, scaling latency |
| Availability | Uptime and failover behavior | Multi-AZ deployment with health checks | Uptime %, MTTR |
| Fault tolerance | Continue operating despite component failures | Circuit breakers, bulkheads, graceful degradation | Fallback success rate, error rate |
| Reliability | Correct operation under expected conditions | Idempotent APIs and safe retries | Success rate, defect rate |
| Observability | Metrics, logs, traces to understand state | Prometheus + Grafana + distributed tracing | Coverage, alert accuracy |
| Operability | Ease of operating and recovering systems | Runbooks, readiness/liveness probes | MTTR, runbook coverage |
| Resilience practices | Techniques to verify robustness | Chaos testing, canary deploys, backpressure | Failure injection results, rollback rate |
| SLO / SLA / Error budget | Defined service targets and budgets | 99.9% availability, 100ms P95 | Error budget burn rate |
| Recovery objectives | Disaster recovery targets | RTO = 15m, RPO = 1h for critical services | RTO / RPO measured via drills |

---

### Structural

| Characteristic | Description | Example | Metrics / Notes |
|---|---|---|---|
| Modularity | Independent, well-scoped components | Microservices or libraries per domain | Number of cross-module dependencies |
| Boundaries / Bounded contexts | Clear domain separation (DDD) | Order vs. Inventory bounded contexts | Cross-context calls, semantic leaks |
| Maintainability | Ease of change and debugging | Layered or hexagonal architecture | Time to implement change, code churn |
| Reusability | Shared components reduce duplication | Auth library used by multiple services | Reuse rate, duplicated implementations |
| Portability | Run across environments with minimal changes | Containerized workloads | Environment parity, deployment failures |
| Testability | Supports unit/integration/contract testing | CI runs unit + contract tests | Test coverage, CI pass rate |
| API & contract management | Versioning and compatibility practices | Consumer-driven contract tests | Breaking change count |
| Data strategy | Consistency model and migration approach | Eventual consistency for caches; migration plans | Replication lag, migration errors |
| Coupling & cohesion | Low interdependence, high internal focus | Well-factored modules, clear interfaces | Coupling metrics, cohesion indicators |

---

### Cross‑Cutting

| Characteristic | Description | Example | Metrics / Notes |
|---|---|---|---|
| Logging & Monitoring | Centralized telemetry and alerting | ELK/Tempo + alert rules | Alert rate, false positive rate |
| Configuration & Secrets | Secure, environment-aware configuration | Vault + env-specific config | Secret rotation interval, breach incidents |
| Error handling & retries | Uniform failure policies and idempotency | Exponential backoff, idempotency keys | Retry success rate, duplicate side-effects |
| Security policies | AuthN, AuthZ, auditing and compliance | RBAC, encryption at rest/in transit | Vulnerability count, audit coverage |
| CI/CD & release practices | Automated build/test/deploy pipelines | Blue/green or canary deployments | Deployment frequency, lead time |
| Governance & standards | ADRs, coding standards, API guidelines | ADRs stored in repo; linting rules | ADR backlog, linting violations |
| Rate limiting & quotas | Protect services from overload | Per-tenant throttles and quotas | Rejection rate, fairness metrics |
| Policy & infra as code | Reproducible infra and policy enforcement | Terraform + policy checks | Drift frequency, policy violations |
| Observability pipelines | Log/metric retention, sampling, cost control | Centralized pipeline with sampling | Ingestion cost, retention coverage |

---

Quick mnemonic (one-liner): Run — Build — Share  
- Run = Operational (how it behaves at runtime)  
- Build = Structural (how it is constructed)  
- Share = Cross‑Cutting (what applies everywhere)

### Easy keyword map to remember
- Operational → Run (latency, availability, SLOs)  
- Structural → Build (modules, boundaries, tests)  
- Cross‑Cutting → Share (logging, config, CI/CD)

## Summary

| Category | Characteristics | Example |
|---|---|---|
| Operational | Performance, Scalability, Availability, Security, Reliability | Streaming service handling peaks |
| Structural | Modularity, Maintainability, Reusability, Portability, Testability | Microservices for e-commerce |
| Cross‑Cutting | Logging, Monitoring, Config Management, Error Handling, Security Policies | Centralized logging & alerting system |

---

See also: Architecture patterns (layered, hexagonal, microservices), design principles (SOLID, DRY), and documentation templates for architecture decision records (ADR).