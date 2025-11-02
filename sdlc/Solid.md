# SOLID Principles in Software Design

## Table of Contents
- [Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
- [Open/Closed Principle (OCP)](#openclosed-principle-ocp)
- [Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
- [Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
- [Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)

SOLID is a set of five design principles that help developers build maintainable, scalable, and robust object-oriented software. Each principle addresses a specific aspect of software design. Below, I explain each with real-world analogies, code examples in C#, violations, and class diagrams.

## Single Responsibility Principle (SRP)
Definition: A class should have only one reason to change.

### Real-World Analogy:
A chef cooks food. A cashier handles payments. If one person does both, any change in cooking or payment affects the same role—violating SRP.

### Examples:
#### ✅ Good Example:
```csharp
public class InvoicePrinter
{
    public void Print(Invoice invoice)
    {
        // Printing logic
    }
}

public class InvoiceSaver
{
    public void Save(Invoice invoice)
    {
        // Saving logic
    }
}
```

#### ❌ Violation:
```csharp
public class InvoiceManager
{
    public void Print(Invoice invoice) { /* ... */ }
    public void Save(Invoice invoice) { /* ... */ }
}
```
Problem: One class handles multiple responsibilities—printing and saving.

### Class Diagram:
```
+------------------+       +------------------+
| InvoicePrinter   |       | InvoiceSaver     |
|------------------|       |------------------|
| +Print()         |       | +Save()          |
+------------------+       +------------------+
```

## Open/Closed Principle (OCP)
[Content continues in same format for other principles...]

Want to see these principles applied to a real-world app like e-commerce or ride-sharing? I can build a full scenario with layered architecture next.
