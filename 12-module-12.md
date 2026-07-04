# Module 12 — Code Quality and Refactoring

## Goal
Safely improve code using IntelliJ refactoring tools.

You will practice Rename, Extract Method, Extract Variable, Inline, Change Signature, Move Class, Safe Delete, Reformat, Optimize Imports, Problems/Inspections, and Git diff review.

## RefactoringDemo.java

Create:

```text
com.example.mavenpractice.refactoring.RefactoringDemo
```

```java
package com.example.mavenpractice.refactoring;

public class RefactoringDemo {

    public static void main(String[] args) {
        String customerName = "Nithakanan";
        double price = 100;
        int quantity = 3;
        double taxRate = 0.13;

        double total = price * quantity;
        double tax = total * taxRate;
        double finalAmount = total + tax;

        System.out.println("Customer: " + customerName);
        System.out.println("Total: " + total);
        System.out.println("Tax: " + tax);
        System.out.println("Final Amount: " + finalAmount);
    }
}
```

## Rename

Shortcut:

```text
Shift + F6
```

Rename:

```text
customerName → buyerName
```

## Extract Method

Select calculation lines and use:

| OS | Shortcut |
|---|---|
| Mac | `Cmd + Option + M` |
| Windows/Linux | `Ctrl + Alt + M` |

Name:

```text
calculateFinalAmount
```

## Extract Variable

Select expression:

```java
price * quantity
```

Use:

| OS | Shortcut |
|---|---|
| Mac | `Cmd + Option + V` |
| Windows/Linux | `Ctrl + Alt + V` |

Name:

```text
subtotal
```

## Inline Variable

| OS | Shortcut |
|---|---|
| Mac | `Cmd + Option + N` |
| Windows/Linux | `Ctrl + Alt + N` |

## Change Signature

Create:

```java
private static void printCustomer(String name) {
    System.out.println("Customer: " + name);
}
```

Use:

| OS | Shortcut |
|---|---|
| Mac | `Cmd + F6` |
| Windows/Linux | `Ctrl + F6` |

Add parameter `String label` and let IntelliJ update usages.

## Move Class

Create package:

```text
com.example.mavenpractice.refactoring.moved
```

Move class using:

```text
F6
```

Then move it back. Do not manually cut/paste.

## Safe Delete

Create:

```java
package com.example.mavenpractice.refactoring;

public class UnusedDemo {
}
```

Use:

```text
Refactor → Safe Delete
```

## Problems and Inspections

Open Problems window and use Quick Fix:

```text
Option + Enter / Alt + Enter
```

## Assignment

```text
1. Create RefactoringDemo
2. Rename customerName to buyerName
3. Extract calculateFinalAmount method
4. Extract subtotal variable
5. Inline one variable
6. Use Change Signature
7. Move class to another package and back
8. Create UnusedDemo
9. Safe Delete UnusedDemo
10. Reformat code
11. Optimize imports
12. Review Git diff
```

When done, reply:

```text
Module 12 completed
```
