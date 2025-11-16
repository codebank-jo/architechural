# Architecural Styles vs Patterns vs Design Patterns

A concise comparison of architectural styles, architectural patterns, and design patterns with examples and illustrative use-cases.

## Comparison table

| Category | Definition | Examples | Illustrative example in practice |
|---|---|---|---|
| Architectural Styles | Broad, high-level structural approaches that define how the overall system is organized. | <ul><li>Monolithic</li><li>Layered (N‑Tier)</li><li>Client‑Server</li><li>Microservices</li><li>Event‑Driven</li><li>Microkernel (Plug‑in)</li><li>Space‑Based</li><li>SOA (Service‑Oriented)</li></ul> | An e‑commerce platform built with a microservices style: separate services for cart, payment, shipping, and catalog deployed independently. |
| Architectural Patterns | Reusable solutions to recurring system‑level problems within an architecture; more concrete than styles but still system‑wide. | <ul><li>MVC</li><li>CQRS</li><li>Event Sourcing</li><li>Broker Pattern</li><li>Publish‑Subscribe</li><li>Master‑Slave</li><li>Blackboard</li></ul> | A web app using MVC: UI (View), business logic (Controller), and data (Model) separated for clearer responsibilities. |
| Design Patterns (Creational) | Patterns focused on object creation mechanisms to decouple system code from how objects are created. | <ul><li>Singleton</li><li>Factory Method</li><li>Abstract Factory</li><li>Builder</li><li>Prototype</li></ul> | A logging utility using Singleton so one instance manages log output and configuration. |
| Design Patterns (Structural) | Patterns that deal with object composition to form flexible structures and relationships between classes. | <ul><li>Adapter</li><li>Decorator</li><li>Proxy</li><li>Composite</li><li>Bridge</li><li>Flyweight</li></ul> | A payment gateway integration using Adapter to present different bank APIs as a uniform interface. |
| Design Patterns (Behavioral) | Patterns focused on communication between objects and distribution of responsibilities. | <ul><li>Observer</li><li>Strategy</li><li>Command</li><li>Template Method</li><li>Mediator</li><li>State</li><li>Chain of Responsibility</li></ul> | A trading dashboard using Observer: when price updates occur, all subscribed views update automatically. |

---

## Key distinctions

- Architectural Styles — macro level: define the overall shape and deployment/communication model of the system (how components are arranged and interact at scale).  
- Architectural Patterns — system-level solutions for recurring architectural problems (concerned with organizing parts of a system to solve specific systemwide needs).  
- Design Patterns — lower-level, language/implementation‑focused solutions to common coding problems (creational, structural, behavioral) used inside components or modules.

---

## How to choose

- Start with a suitable Architectural Style for constraints (team size, operational needs, latency, deployment).  
- Apply Architectural Patterns to solve system‑level concerns (consistency, communication, scaling).  
- Use Design Patterns within services/modules to keep code maintainable, testable, and extensible.

---