# 🧪 Test-Driven Development (TDD) in C#

## 🔍 What is TDD?
TDD is a development technique where you:

1. Write a test for a new feature
2. Run the test (it fails)
3. Write the minimal code to pass the test
4. Refactor the code
5. Repeat

## ✅ Why use TDD?
- Ensures code correctness
- Drives clean architecture
- Reduces regression bugs
- Encourages modular design

## 🧑‍💻 TDD Example in C# (using xUnit)

### Step 1: Write a failing test
```csharp
// CalculatorTests.cs
using Xunit;

public class CalculatorTests
{
    [Fact]
    public void Add_TwoNumbers_ReturnsSum()
    {
        var calculator = new Calculator();
        var result = calculator.Add(2, 3);
        Assert.Equal(5, result);
    }
}
```

### Step 2: Write minimal code to pass the test
```csharp
// Calculator.cs
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }
}
```

# 🤝 Behavior-Driven Development (BDD) in C#

## 🔍 What is BDD?
BDD focuses on behavior and collaboration. It uses natural language to describe how the system should behave, often with tools like SpecFlow in C#.

## ✅ Why use BDD?
- Improves communication between devs, testers, and business
- Makes requirements executable
- Bridges gap between technical and non-technical stakeholders

## 🧑‍💻 BDD Example in C# (using SpecFlow)

### Feature File (Addition.feature)
```gherkin
Feature: Calculator
  Scenario: Add two numbers
    Given I have entered 2 and 3 into the calculator
    When I press add
    Then the result should be 5
```

### Step Definitions (CalculatorSteps.cs)
```csharp
using TechTalk.SpecFlow;
using Xunit;

[Binding]
public class CalculatorSteps
{
    private int _a, _b, _result;
    private Calculator _calculator = new Calculator();

    [Given(@"I have entered (.*) and (.*) into the calculator")]
    public void GivenIHaveEnteredNumbers(int a, int b)
    {
        _a = a;
        _b = b;
    }

    [When(@"I press add")]
    public void WhenIPressAdd()
    {
        _result = _calculator.Add(_a, _b);
    }

    [Then(@"the result should be (.*)")]
    public void ThenTheResultShouldBe(int expected)
    {
        Assert.Equal(expected, _result);
    }
}
```

# ⚖️ TDD vs BDD in C#

| Feature      | TDD                               | BDD                               |
|--------------|-----------------------------------|-----------------------------------|
| Focus        | Code correctness                  | System behavior and business expectations |
| Language     | C# test frameworks (xUnit, NUnit) | Gherkin + SpecFlow                |
| Stakeholders | Developers                         | Developers, QA, Business Analysts |
| Test Style   | Unit tests                        | Acceptance tests                  |
| Tools        | xUnit, NUnit, MSTest             | SpecFlow, Gherkin                 |

# 🧭 When to Use What
**Use TDD when:**
- Building internal logic, APIs, or libraries
- You want fast feedback during development
- You’re working in a dev-heavy team

**Use BDD when:**
- Building user-facing features
- Collaborating with QA and business teams
