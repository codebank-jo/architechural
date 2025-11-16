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
- Restaurant: Chef cooks; cashier handles payments.  
- Library: Librarian catalogs books; security handles entry.

### Class Diagram (HTML)
<div style="display:flex;gap:16px;">
  <div style="border:1px solid #333;padding:8px;width:160px;text-align:center;">
    <div style="font-weight:bold;">InvoicePrinter</div>
    <hr/>
    <div>+ Print()</div>
  </div>
  <div style="border:1px solid #333;padding:8px;width:160px;text-align:center;">
    <div style="font-weight:bold;">InvoiceSaver</div>
    <hr/>
    <div>+ Save()</div>
  </div>
</div>

### C# Example
```csharp
public class Invoice { public int Id; public decimal Amount; }

public class InvoiceSaver
{
    public void Save(Invoice invoice)
    {
        // persist invoice (DB/file)
    }
}

public class InvoicePrinter
{
    public void Print(Invoice invoice)
    {
        // formatting and send to printer
    }
}

// Client
var invoice = new Invoice { Id = 1, Amount = 99.95m };
new InvoiceSaver().Save(invoice);
new InvoicePrinter().Print(invoice);
```

---

## Open/Closed Principle (OCP)
Definition: Software entities should be open for extension but closed for modification.

### Real-World Analogy:
- Power outlet / plugs: New appliances plug in without changing the outlet.  
- Shipping containers: New container types fit existing handling infrastructure.

### Class Diagram (HTML)
<div style="display:flex;align-items:center;gap:12px;">
  <div style="border:1px solid #333;padding:8px;width:180px;text-align:center;">
    <div style="font-weight:bold;">IDiscountStrategy</div>
  </div>
  <div style="display:flex;flex-direction:column;gap:8px;">
    <div style="border:1px solid #333;padding:8px;width:160px;text-align:center;">
      <div style="font-weight:bold;">SeasonalDiscount</div>
    </div>
    <div style="border:1px solid #333;padding:8px;width:160px;text-align:center;">
      <div style="font-weight:bold;">ClearanceDiscount</div>
    </div>
  </div>
  <div style="border:1px solid #333;padding:8px;width:200px;text-align:center;margin-left:12px;">
    <div style="font-weight:bold;">OrderProcessor</div>
    <hr/>
    <div>-> IDiscountStrategy</div>
  </div>
</div>

### C# Example
```csharp
public interface IDiscountStrategy { decimal Apply(decimal amount); }

public class NoDiscount : IDiscountStrategy { public decimal Apply(decimal a) => a; }
public class SeasonalDiscount : IDiscountStrategy { public decimal Apply(decimal a) => a * 0.9m; }

public class OrderProcessor
{
    private readonly IDiscountStrategy _discount;
    public OrderProcessor(IDiscountStrategy discount) => _discount = discount;
    public decimal Total(decimal amount) => _discount.Apply(amount);
}

// Client: add new strategy without changing OrderProcessor
var processor = new OrderProcessor(new SeasonalDiscount());
var total = processor.Total(200m); // 180.0
```

---

## Liskov Substitution Principle (LSP)
Definition: Subtypes must be substitutable for their base types without altering program correctness.

### Real-World Analogy:
- Replacement batteries: A AA rechargeable can substitute a disposable AA.  
- Vehicle rental: A compact car can substitute a midsize car if it meets the required contract.

### Class Diagram (HTML)
<div style="display:flex;gap:12px;align-items:flex-start;">
  <div style="border:1px solid #333;padding:8px;width:160px;text-align:center;">
    <div style="font-weight:bold;">Shape</div>
  </div>
  <div style="display:flex;flex-direction:column;gap:8px;margin-left:8px;">
    <div style="border:1px solid #333;padding:8px;width:160px;text-align:center;">
      <div style="font-weight:bold;">Rectangle</div>
    </div>
    <div style="border:1px solid #333;padding:8px;width:160px;text-align:center;">
      <div style="font-weight:bold;">Circle</div>
    </div>
  </div>
</div>

### C# Example
```csharp
public abstract class Shape { public abstract double Area(); }

public class Rectangle : Shape
{
    public double Width { get; set; }
    public double Height { get; set; }
    public override double Area() => Width * Height;
}

public class Circle : Shape
{
    public double Radius { get; set; }
    public override double Area() => Math.PI * Radius * Radius;
}

// Client uses base type
IEnumerable<Shape> shapes = new Shape[] {
    new Rectangle { Width = 3, Height = 4 },
    new Circle { Radius = 2 }
};

foreach (var s in shapes) Console.WriteLine(s.Area());
```

---

## Interface Segregation Principle (ISP)
Definition: Clients should not be forced to depend on interfaces they do not use; prefer many small, specific interfaces.

### Real-World Analogy:
- Toolbelt vs full toolbox: carry only needed tools.  
- Reception kiosk vs full-service counter: only required capabilities are exposed.

### Class Diagram (HTML)
<div style="display:flex;gap:12px;align-items:center;">
  <div style="border:1px solid #333;padding:8px;width:120px;text-align:center;">
    <div style="font-weight:bold;">IPrinter</div>
  </div>
  <div style="border:1px solid #333;padding:8px;width:120px;text-align:center;">
    <div style="font-weight:bold;">IScanner</div>
  </div>
  <div style="border:1px solid #333;padding:8px;width:160px;text-align:center;margin-left:12px;">
    <div style="font-weight:bold;">SimplePrinter</div>
  </div>
  <div style="border:1px solid #333;padding:8px;width:180px;text-align:center;">
    <div style="font-weight:bold;">MultiFunctionDevice</div>
  </div>
</div>

### C# Example
```csharp
public interface IPrinter { void Print(Document d); }
public interface IScanner { void Scan(Document d); }

public class SimplePrinter : IPrinter
{
    public void Print(Document d) { /* print only */ }
}

public class MultiFunctionDevice : IPrinter, IScanner
{
    public void Print(Document d) { /* print */ }
    public void Scan(Document d) { /* scan */ }
}

// Client uses only the printing interface
IPrinter printer = new SimplePrinter();
printer.Print(new Document());
```

---

## Dependency Inversion Principle (DIP)
Definition: High-level modules should not depend on low-level modules; both should depend on abstractions.

### Real-World Analogy:
- Power adapters: devices rely on the adapter interface, not the power plant.  
- Universal remote: controls devices via a protocol, not a specific model.

### Class Diagram (HTML)
<div style="display:flex;gap:12px;align-items:center;">
  <div style="border:1px solid #333;padding:8px;width:140px;text-align:center;">
    <div style="font-weight:bold;">ILogger</div>
  </div>
  <div style="display:flex;flex-direction:column;gap:8px;">
    <div style="border:1px solid #333;padding:8px;width:160px;text-align:center;">
      <div style="font-weight:bold;">FileLogger</div>
    </div>
    <div style="border:1px solid #333;padding:8px;width:160px;text-align:center;">
      <div style="font-weight:bold;">ConsoleLogger</div>
    </div>
  </div>
  <div style="border:1px solid #333;padding:8px;width:180px;text-align:center;margin-left:12px;">
    <div style="font-weight:bold;">UserService</div>
    <hr/>
    <div>-> ILogger</div>
  </div>
</div>

### C# Example
```csharp
public interface ILogger { void Log(string message); }

public class FileLogger : ILogger
{
    public void Log(string message) { /* write to file */ }
}

public class UserService
{
    private readonly ILogger _logger;
    public UserService(ILogger logger) => _logger = logger;
    public void Create(string name)
    {
        // create user...
        _logger.Log($"User {name} created");
    }
}

// Client wiring (manual DI)
ILogger logger = new FileLogger();
var service = new UserService(logger);
service.Create("alice");
```

These examples show small, testable components and simple client code demonstrating usage and substitutability. Apply patterns pragmatically — prefer clarity over over-engineering.
