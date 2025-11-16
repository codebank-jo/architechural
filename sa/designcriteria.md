# Architecture Design Criteria

Architecture design criteria are the guiding principles and constraints that shape how a software system is structured. These criteria ensure the architecture aligns with both business needs and technical realities.

---

## Architecture Design Criteria Table

| Criterion | Category | Description | Example impact on architecture |
|---|---|---|---|
| Business Objectives | Business | Strategic goals the system must support. | Choose a scalable architecture to meet growth targets. |
| Functional Requirements | Functional | Specific features or capabilities the system must provide. | Define service boundaries and API contracts. |
| Non-Functional Requirements (NFRs) | Quality Attributes | Performance, availability, scalability, etc. | Use caching, load balancing, or distributed systems. |
| Technical Constraints | Technical | Limitations from existing systems, tools, or environments. | Must integrate with legacy ERP; restricts tech choices. |
| Regulatory & Compliance | Legal / Compliance | Standards the system must adhere to (e.g., GDPR, PCI‑DSS). | Enforce encryption, audit logs, and retention policies. |
| Portability | Deployment | Ability to run across different platforms/environments. | Use containers and cloud‑agnostic services. |
| Security | Quality Attributes | Protect data and prevent unauthorized access. | Implement authentication, authorization, and encryption. |
| Maintainability | Quality Attributes | Ease of updating, debugging, and extending the system. | Favor modular design and separation of concerns. |
| Interoperability | Integration | Ability to work with other systems and technologies. | Use standard protocols (REST, gRPC) and formats (JSON, XML). |
| Cost-effectiveness | Business/Technical | Balance performance/features with budget constraints. | Choose open-source tools or cloud services with cost control. |

---

## Why these criteria matter

- Ensure architecture aligns with business strategy and priorities.  
- Help manage trade-offs between performance, cost, and flexibility.  
- Provide a repeatable framework for evaluating architectural decisions.  
- Make trade-offs explicit for stakeholders (e.g., faster time-to-market vs. long-term maintainability).

---

## Architecturally Significant Requirements (ASRs)

### What is an ASR?

**Definition:** An Architecturally Significant Requirement (ASR) is a requirement that has a direct impact on the architecture of a system.

**Key Idea:** Not all requirements influence architecture — only those that affect structure, design decisions, or quality attributes are considered ASRs.

**Examples:**
- Performance: "System must handle 10,000 concurrent users."
- Security: "System must comply with GDPR and encrypt all sensitive data."
- Scalability: "System must support global deployment across multiple regions."
- Availability: "System must achieve 99.99% uptime."

---

### Types of ASRs

#### Functional ASRs
Rare, but sometimes a functional requirement can shape architecture.

**Example:** "System must support real-time video streaming."

#### Non-Functional ASRs (Quality Attributes)
Most ASRs are non-functional requirements.

**Examples:** performance, reliability, scalability, security, maintainability, portability.

#### Constraints
Technical or business constraints that restrict design choices.

**Example:** "Must run on AWS cloud only."

---

### Why ASRs Matter

- **Drive architectural decisions:** They determine whether to use monolith, microservices, event-driven, or layered styles.
- **Prioritize trade-offs:** Architects balance ASRs (e.g., performance vs cost, security vs usability).
- **Ensure alignment:** Architecture reflects business drivers and compliance needs.
- **Reduce risk:** Identifying ASRs early prevents costly redesigns later.

---

### Example Scenario: Banking System

Imagine designing a banking system:

**Business Requirement:** Customers must transfer money online.

**ASRs:**
- Security: Must comply with PCI-DSS and encrypt transactions.
- Availability: Must achieve 99.99% uptime.
- Performance: Transactions must complete in <2 seconds.

**Impact:** These ASRs drive choices like distributed architecture, redundant servers, encryption layers, and load balancing.

---

## Architectural Styles Decision Matrix

| Design criterion | Monolithic | Layered (N‑Tier) | Microservices | Event‑Driven | SOA |
|---|---:|---:|---:|---:|---:|
| Business objectives alignment | Medium | High | High | High | High |
| Functional requirements fit | High | High | High | Medium | High |
| Non-functional requirements | Low–Medium | Medium | High | High | Medium–High |
| Scalability | Low | Medium | High | High | Medium |
| Maintainability | Low | Medium | High | Medium | Medium |
| Security | Medium | High | Medium–High | Medium | High |
| Portability | Low | Medium | High | High | Medium |
| Interoperability | Low | Medium | High | High | Very High |
| Regulatory & compliance | Medium | High | Medium–High | Medium | High |
| Technical constraints handling | Low–Medium | Medium | High | Medium | High |
| Cost‑effectiveness (initial) | High | Medium | Medium–Low | Medium | Medium |

---

## Key takeaways

- **Monolithic:** Simple and cost‑effective for small apps, but limited scalability and long‑term maintainability.  
- **Layered (N‑Tier):** Balanced and familiar; good separation of concerns for enterprise apps.  
- **Microservices:** Best for scalability and independent delivery; requires strong operational investment.  
- **Event‑Driven:** Excellent for decoupling and responsiveness; adds complexity for tracing and consistency.  
- **SOA:** Strong interoperability for large enterprises; can be heavyweight (ESB risks).

---

## How to Use This Guide

1. **Identify ASRs:** Work with stakeholders to discover architecturally significant requirements.
2. **Document trade-offs:** Note which ASRs are most critical and why.
3. **Reference the matrix:** Use the decision matrix to evaluate candidate architectural styles.
4. **Document decisions:** Record which criteria drove your final architectural choice.

Use this matrix and criteria as a checklist when evaluating or recommending architectural styles — document assumptions, constraints, and which criteria drove the final decision.