# Module 11 — Unit Testing with JUnit

## Goal
Learn how to create, run, debug, and review JUnit tests inside IntelliJ IDEA.

You will practice adding JUnit dependency, creating tests from a class, running single/all tests, debugging tests, reading failed assertions, running Maven `test`, and coverage.

## Use Maven Project

Use:

```text
maven-practice
```

## Add JUnit Dependency

In `pom.xml`:

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.10.2</version>
    <scope>test</scope>
</dependency>
```

Reload Maven.

## Calculator.java

```java
package com.example.mavenpractice;

public class Calculator {

    public int add(int first, int second) {
        return first + second;
    }

    public int subtract(int first, int second) {
        return first - second;
    }

    public int multiply(int first, int second) {
        return first * second;
    }

    public int divide(int first, int second) {
        if (second == 0) {
            throw new IllegalArgumentException("Cannot divide by zero");
        }

        return first / second;
    }
}
```

## Create Test from Class

Open `Calculator.java` and use:

| OS | Shortcut |
|---|---|
| Mac | `Cmd + Shift + T` |
| Windows/Linux | `Ctrl + Shift + T` |

Choose:

```text
Create New Test → JUnit 5 → CalculatorTest
```

## CalculatorTest.java

```java
package com.example.mavenpractice;

import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    private final Calculator calculator = new Calculator();

    @Test
    void shouldAddTwoNumbers() {
        int result = calculator.add(10, 5);
        assertEquals(15, result);
    }

    @Test
    void shouldSubtractTwoNumbers() {
        int result = calculator.subtract(10, 5);
        assertEquals(5, result);
    }

    @Test
    void shouldMultiplyTwoNumbers() {
        int result = calculator.multiply(10, 5);
        assertEquals(50, result);
    }

    @Test
    void shouldDivideTwoNumbers() {
        int result = calculator.divide(10, 5);
        assertEquals(2, result);
    }

    @Test
    void shouldThrowExceptionWhenDividingByZero() {
        IllegalArgumentException exception = assertThrows(
                IllegalArgumentException.class,
                () -> calculator.divide(10, 0)
        );

        assertEquals("Cannot divide by zero", exception.getMessage());
    }
}
```

## Run and Debug Tests

Use gutter icons beside test method/class.

Debug a test by clicking the bug icon or running in Debug mode. Add breakpoint inside `divide` and inspect values.

## Failed Test Practice

Temporarily change:

```java
assertEquals(999, result);
```

Run and inspect expected vs actual. Fix it back.

## Coverage

Right-click test class:

```text
Run 'CalculatorTest' with Coverage
```

Review covered lines.

## Maven Test

Maven tool window:

```text
Lifecycle → test
```

or terminal:

```bash
mvn test
```

## Assignment

```text
1. Add JUnit dependency
2. Reload Maven
3. Create Calculator
4. Generate CalculatorTest using Cmd/Ctrl Shift T
5. Add tests for add/subtract/multiply/divide
6. Add exception test for divide by zero
7. Run single test
8. Run test class
9. Debug divide test
10. Create failed test and inspect output
11. Fix failed test
12. Run Maven test
13. Run with coverage
```

When done, reply:

```text
Module 11 completed
```
