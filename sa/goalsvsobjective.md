# Goals vs Objectives

## Definitions

| Term | Meaning | Example in Software Project |
|---|---|---|
| Business Requirements | High-level needs or conditions the system must satisfy to deliver value to the business. | "The system must allow customers to place online orders." |
| Business Goals | Broad, long-term outcomes the organization wants to achieve. | "Increase online sales by 20% in the next year." |
| Business Drivers | External or internal forces that motivate the project (why it’s needed). | Market competition, regulatory compliance, customer demand for mobile access. |
| Business Objectives | Specific, measurable steps to achieve goals. | "Reduce checkout time to under 2 minutes." |

---

## Why They Matter in Software Architecture

- Alignment with business strategy — Architecture must serve business objectives (e.g., choose microservices if scalability is a goal).  
- Prioritization of features — Requirements and drivers help decide what is essential (e.g., GDPR forces privacy controls).  
- Risk management — Drivers reveal risks to address in the design (e.g., uptime driver → redundancy and failover).  
- Measurable success — Objectives provide metrics to evaluate architecture (e.g., "checkout under 2 minutes" drives caching and performance work).

---

## Example Scenario

- Business Requirement: Customers must be able to browse and purchase products online.  
- Business Goal: Increase customer retention and sales.  
- Business Driver: Competitors offer faster mobile shopping experiences.  
- Business Objective: Achieve 99.9% uptime and reduce cart abandonment by 15%.

Implication: adopt microservices for scalability, event-driven design for responsiveness, and cloud deployment for higher availability.

---

## Key Takeaway

Requirements, goals, drivers, and objectives provide the business context that guides architecture decisions. Without them, architecture risks being "technology for technology’s sake" instead of solving real business problems.

They ensure the system is relevant, valuable, and sustainable for the organization.