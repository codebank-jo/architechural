# What Is Software Design

Software design translates requirements into a blueprint for implementation. It covers:
- Architectural design — high-level structure and component interactions
- Detailed design — data structures, algorithms, and internal logic
- Interface design — module and external system contracts

Design bridges the problem domain and the solution domain.

# Why Change in Software Is Inevitable

Software evolves because:
- User needs change
- Business goals shift
- Platforms and tools advance
- Bugs and performance issues arise
- Regulations and security requirements evolve

This leads to software entropy unless systems are actively maintained.

# Design Principles and Why Use Them

Design principles guide creation of systems that are:
- Maintainable
- Scalable
- Understandable
- Testable

Common principles:
- Single Responsibility Principle (SRP): a module has one reason to change  
- Open/Closed Principle: open for extension, closed for modification  
- Liskov Substitution Principle: subtypes replace their base types without breaking behavior  
- Interface Segregation Principle: prefer many focused interfaces over a single large one  
- Dependency Inversion Principle: depend on abstractions, not concretes

These reduce complexity and improve robustness.

# Coupling and Cohesion

Definitions:
- Coupling: degree of interdependence between modules (low is better)  
- Cohesion: degree to which elements within a module belong together (high is better)

Why it matters:
- Low coupling + high cohesion → easier to change, test, and reuse
- High coupling or low cohesion → fragile, hard-to-maintain code

# Categories of Principles

## Object-Oriented Design (SOLID)
- SRP, OCP, LSP, ISP, DIP — promotes modular, testable classes

## Architectural Principles
- Separation of Concerns, Modularity, Encapsulation, Scalability, Resilience

## Agile-related Principles
- Customer collaboration, responding to change, short delivery cycles, sustainable pace

## Testing Principles
- Test early and often, automate where practical, test behavior not implementation, keep tests independent

## General Engineering Principles
- DRY (Don’t Repeat Yourself)  
- KISS (Keep It Simple, Stupid)  
- YAGNI (You Aren’t Gonna Need It)  
- Law of Demeter (only talk to immediate friends)

# Practical Guidance

- Prefer small, focused modules with clear contracts.  
- Design for testability (dependency injection, seams for integration).  
- Use evolution-friendly patterns (composition over inheritance, anti-corruption layers).  
- Apply the simplest pattern that meets current needs; refactor as requirements evolve.  
- Balance upfront design and incremental discovery: lightweight intent and guardrails work best with iterative delivery.

# Role of Design in Delivery

Design provides guardrails, reuse patterns, and a shared vocabulary. Architects and senior engineers should:
- Communicate high-level intent and constraints
- Review and coach on risky areas
- Enable teams to evolve the design incrementally
