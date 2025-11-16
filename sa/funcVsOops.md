# Functional vs Object-Oriented Programming

## Table of Contents
- [Mutable vs Immutable](#mutable-vs-immutable)  
- [Object-Oriented Programming (OOP)](#object-oriented-programming-oop)  
- [Functional Programming (FP)](#functional-programming-fp)  
- [Comparison](#comparison)  
- [Key Takeaways](#key-takeaways)

---

## Mutable vs Immutable

### Mutable

**Definition:** A mutable object's state can be changed after it is created.

**Pros:**
- Easy to update values directly.
- Familiar to most developers.
- Lower memory overhead (no new objects).

**Cons:**
- Risk of unintended side effects, especially in concurrent programs.
- Harder to reason about object history.
- Difficult to debug state changes.

**Example (C# Mutable Class):**
```csharp
public class Person
{
    public string Name { get; set; }   // Mutable property
    public int Age { get; set; }       // Mutable property
}

class Program
{
    static void Main()
    {
        var person = new Person { Name = "Alice", Age = 25 };
        person.Age = 26;   // State changed directly
        Console.WriteLine($"{person.Name} is now {person.Age} years old.");
        // Output: Alice is now 26 years old.
    }
}
```

**Key Point:** The `Age` property is mutable — you can change it after object creation.

---

### Immutable

**Definition:** An immutable object's state cannot be changed once it is created.

**Pros:**
- Safer and more predictable (what you see is what you get).
- Thread-safe by design (no locks needed).
- Easier to reason about and debug.
- Natural fit for functional programming.

**Cons:**
- Requires creating new objects for updates (memory overhead).
- May feel verbose for simple updates.
- Requires discipline and language support.

**Example (C# Immutable Class):**
```csharp
public class Person
{
    public string Name { get; }
    public int Age { get; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Method returns a new Person with updated age
    public Person Birthday()
    {
        return new Person(Name, Age + 1);
    }
}

class Program
{
    static void Main()
    {
        var person = new Person("Alice", 25);
        var olderAlice = person.Birthday(); // Creates new object
        Console.WriteLine($"{olderAlice.Name} is now {olderAlice.Age} years old.");
        // Output: Alice is now 26 years old.
    }
}
```

**Key Point:** `Person` is immutable — you can't change properties directly; instead, you create a new object.

---

## Object-Oriented Programming (OOP)

**Definition:** Organizes code around objects that encapsulate both data and behavior.

**Core Concepts:**
- Encapsulation — bundle data and methods together.
- Inheritance — extend base classes.
- Polymorphism — use base types for different implementations.
- Abstraction — hide complex details behind interfaces.

**Languages:** C#, Java, Python, C++.

**Example (C# OOP):**
```csharp
public class BankAccount
{
    public string AccountHolder { get; private set; }
    public decimal Balance { get; private set; }

    public BankAccount(string holder)
    {
        AccountHolder = holder;
        Balance = 0;
    }

    public void Deposit(decimal amount)
    {
        if (amount > 0)
            Balance += amount;
    }

    public void Withdraw(decimal amount)
    {
        if (amount > 0 && amount <= Balance)
            Balance -= amount;
    }
}

class Program
{
    static void Main()
    {
        var account = new BankAccount("Alice");
        account.Deposit(100);
        account.Withdraw(30);
        Console.WriteLine($"Balance: ${account.Balance}");
        // Output: Balance: $70
    }
}
```

**Key Point:** State (Balance) is stored inside the object and modified by methods.

---

## Functional Programming (FP)

**Definition:** Focuses on pure functions, immutability, and avoiding side effects.

**Core Concepts:**
- Pure functions — same input always produces same output; no side effects.
- Higher-order functions — functions that take or return other functions.
- Immutability — data never changes; functions return new data.
- Recursion — prefer recursion over loops.

**Languages:** Haskell, F#, Scala, JavaScript (functional style), C# (LINQ, delegates).

**Example (C# FP style):**
```csharp
public static class BankAccountFunctions
{
    public static (decimal balance, string message) Deposit(decimal balance, decimal amount)
    {
        return amount > 0
            ? (balance + amount, $"Deposited ${amount}. New balance: ${balance + amount}")
            : (balance, "Invalid amount");
    }

    public static (decimal balance, string message) Withdraw(decimal balance, decimal amount)
    {
        return amount > 0 && amount <= balance
            ? (balance - amount, $"Withdrew ${amount}. New balance: ${balance - amount}")
            : (balance, "Invalid transaction");
    }
}

class Program
{
    static void Main()
    {
        decimal balance = 0;
        (balance, var msg1) = BankAccountFunctions.Deposit(balance, 100);
        Console.WriteLine(msg1);
        (balance, var msg2) = BankAccountFunctions.Withdraw(balance, 30);
        Console.WriteLine(msg2);
        Console.WriteLine($"Final balance: ${balance}");
    }
}
```

**Key Point:** Functions operate on immutable data and return new values instead of modifying state.

---

## Comparison

| Aspect | Mutable | Immutable | OOP | FP |
|---|---|---|---|---|
| **Definition** | State can change after creation | State cannot change | Organizes around objects | Organizes around pure functions |
| **Update mechanism** | Modify existing object | Create new object | Methods modify object state | Functions return new values |
| **Encapsulation** | Data + behavior in object | Read-only properties | Strong encapsulation | Data passed to functions |
| **Concurrency** | Requires synchronization | Safe by design | Locks / coordination needed | No shared mutable state |
| **Testing** | Need to track state history | Easier (no state side effects) | Depends on design | Easier (pure functions) |
| **Memory** | Lower (in-place updates) | Higher (new objects) | Variable | Variable |
| **Learning curve** | Familiar | Requires mindset shift | Intuitive for modeling entities | Steep for OOP developers |
| **C# Example** | `person.Age = 26;` | `new Person(Name, Age+1)` | `account.Withdraw(50)` | `Withdraw(balance, 50)` |

---

## When to use which

### Use OOP when:
- Modeling real-world entities (users, accounts, products).
- Team is familiar with OOP patterns and practices.
- Building large systems with many interacting objects.
- Inheritance hierarchies make sense for domain modeling.

### Use FP when:
- Processing data transformations and pipelines.
- Concurrency and thread-safety are critical.
- Easy testability and predictability matter.
- Avoiding state mutations is a requirement.

### Use Immutability when:
- Building distributed or concurrent systems.
- You need reliable debugging and auditing.
- Performance is less critical than safety.

### Use Mutability when:
- Performance is critical (low-latency systems).
- State updates are frequent and localized.
- Working in single-threaded contexts.

---

## Key Takeaways

| Concept | Summary |
|---|---|
| **Mutable vs Immutable** | Mutable objects change state; immutable objects never change, they produce new versions. |
| **OOP** | Models software as interacting objects with data and behavior; encourages encapsulation and inheritance. |
| **FP** | Models software as transformations of data through pure functions; encourages immutability and composability. |
| **In Practice** | Most modern languages (C#, Python, JavaScript, Scala) support both paradigms; choose based on context. |
| **Hybrid Approach** | Combine OOP for domain modeling with FP principles (immutability, pure functions) for safer, testable code. |

---

## C# Examples Summary

**OOP approach:** Objects own state; methods modify state internally.

**FP approach:** Functions are stateless; they receive data and return transformed data.

**Hybrid approach:** Use immutable objects with functional transformations (LINQ, delegates) for balance.