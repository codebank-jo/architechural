# What Is Software Design

Software design translates requirements into a blueprint for implementation. It includes:
- Architectural design — high-level structure and component interactions  
- Detailed design — data structures, algorithms, and internal logic  
- Interface design — module and external system contracts

Design bridges the problem domain and the solution domain.

---

# Why Change in Software Is Inevitable

Software evolves because:
- User needs change  
- Business goals shift  
- Platforms and tools advance  
- Bugs and performance issues arise  
- Regulations and security requirements evolve

Without active maintenance systems accrue entropy and technical debt.

---

# Design Principles (quick reference)

| Principle | Short description | Why it matters |
|---|---|---|
| Single Responsibility (SRP) | A module has one reason to change | Reduces coupling, improves testability |
| Open/Closed (OCP) | Open for extension, closed for modification | Enables adding features with minimal risk |
| Liskov Substitution (LSP) | Subtypes can replace base types safely | Preserves correctness when substituting types |
| Interface Segregation (ISP) | Many small, client-specific interfaces | Avoids forcing clients to implement unused APIs |
| Dependency Inversion (DIP) | Depend on abstractions, not concretes | Improves replaceability and testability |

---

# Coupling and Cohesion

| Concept | Definition | Target |
|---|---:|---|
| Coupling | Degree of interdependence between modules | Low (loose) coupling is better |
| Cohesion | Degree to which elements within a module belong together | High cohesion is better |

Why this matters: Low coupling + high cohesion → easier to change, test, and reuse. High coupling or low cohesion → fragile and costly to evolve.

---

# Categories of Principles

| Category | Examples / Focus |
|---|---|
| Object-oriented design | SOLID (SRP, OCP, LSP, ISP, DIP) |
| Architectural | Separation of concerns, modularity, scalability, resilience |
| Agile-related | Short feedback cycles, incremental design, continuous improvement |
| Testing | Test early, automate, keep tests independent |
| Engineering | DRY, KISS, YAGNI, Law of Demeter |

---

# Practical Guidance

- Prefer small, focused modules with clear contracts.  
- Design for testability: dependency injection, seams for integration.  
- Favor composition over inheritance; use anti-corruption layers at boundaries.  
- Apply the simplest pattern that meets current needs; refactor as requirements evolve.  
- Balance upfront design and incremental discovery: lightweight intent + guardrails works well with iterative delivery.  
- Measure outcomes (cycle time, lead time, defect rate) to validate design decisions.

---

# Role of Design in Delivery

| Actor | Contribution |
|---|---|
| Architects / Tech leads | Communicate vision and constraints; define reusable patterns |
| Teams | Evolve design incrementally; implement tests and observability |
| QA / DevOps | Validate design with CI/CD, automated tests, and monitoring |

Design should provide guardrails and enable teams to deliver safely and repeatedly.

---

# Short checklist for a design review

- Is responsibility clear and bounded?  
- Are abstractions stable and minimal?  
- Can components be tested in isolation?  
- Is coupling minimized and cohesion maximized?  
- Is the change path (extension) clear without modifying core code?  
- Are operational concerns (observability, recovery) addressed?

--- 

Further reading: refer to SOLID, architecture patterns (layered, hexagonal, event-driven), and the SDLC overview (sdlc/SoftwareDevelopmentLifeCycle.md).
