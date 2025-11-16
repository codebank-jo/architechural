# 🧪 Test-Driven Development (TDD) in C#

TDD is a development technique with a short feedback loop:
1. Write a test for a new behavior.
2. Run the test (it fails).
3. Write the minimal code to make the test pass.
4. Refactor.
5. Repeat.

## Why use TDD
- Ensures correctness via executable tests.  
- Encourages modular, testable design.  
- Reduces regressions and supports refactoring.

## Example (xUnit)

Step 1 — failing test:
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

Step 2 — minimal implementation:
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

# Behavior-Driven Development (BDD) in C#

BDD focuses on observable behavior and collaboration, using human-readable specifications (e.g., Gherkin) that map to automated tests.

## Why use BDD
- Improves communication between developers, QA, and business stakeholders.  
- Makes requirements executable and verifiable.  
- Useful for acceptance-level tests and examples.

## Example (SpecFlow)

Feature file:
```gherkin
Feature: Calculator
  Scenario: Add two numbers
    Given I have entered 2 and 3 into the calculator
    When I press add
    Then the result should be 5
```

Step definitions:
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

# TDD vs BDD

| Feature      | TDD                          | BDD                                 |
|--------------|------------------------------|-------------------------------------|
| Focus        | Implementation and unit logic| System behavior and acceptance      |
| Language     | Test framework code (C#)     | Gherkin + step definitions          |
| Stakeholders | Developers                   | Developers, QA, Business Analysts   |
| Test style   | Unit tests                   | Acceptance / scenario tests         |
| Tools        | xUnit, NUnit, MSTest         | SpecFlow (C#), Gherkin              |

# When to use which

Use TDD when:
- Building libraries, algorithms, or internal logic.
- You need fast, low‑level feedback.

Use BDD when:
- Defining user-facing features and acceptance criteria.
- Collaborating with non-technical stakeholders to validate behavior.
