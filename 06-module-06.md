# Module 06 — Debugging from Zero

## Goal
Learn IntelliJ debugging from the beginning.

You will practice breakpoints, Debug mode, Step Over, Step Into, Step Out, Resume, Variables, Watches, Evaluate Expression, and conditional breakpoints.

## Package

```text
com.example.debugging
```

Create:

```text
DebugDemo
BugDemo
ConditionalBreakpointDemo
```

## DebugDemo.java

```java
package com.example.debugging;

public class DebugDemo {

    public static void main(String[] args) {
        int price = 100;
        int quantity = 3;

        int total = calculateTotal(price, quantity);

        System.out.println("Total = " + total);
    }

    private static int calculateTotal(int price, int quantity) {
        int result = price * quantity;
        return result;
    }
}
```

Add breakpoint on:

```java
int total = calculateTotal(price, quantity);
```

Debug:

| OS | Shortcut |
|---|---|
| Mac | `Ctrl + D` |
| Windows/Linux | `Shift + F9` |

## Debug Shortcuts

| Action | Mac | Windows/Linux |
|---|---|---|
| Toggle breakpoint | `Cmd + F8` | `Ctrl + F8` |
| View breakpoints | `Cmd + Shift + F8` | `Ctrl + Shift + F8` |
| Step Over | `F8` | `F8` |
| Step Into | `F7` | `F7` |
| Step Out | `Shift + F8` | `Shift + F8` |
| Resume | `Cmd + Option + R` | `F9` |
| Evaluate Expression | `Option + F8` | `Alt + F8` |

## BugDemo.java

```java
package com.example.debugging;

public class BugDemo {

    public static void main(String[] args) {
        int[] numbers = {10, 20, 30};

        int total = 0;

        for (int i = 0; i <= numbers.length; i++) {
            total = total + numbers[i];
        }

        System.out.println("Total = " + total);
    }
}
```

Bug:

```text
i <= numbers.length
```

Fix:

```text
i < numbers.length
```

Use debugger to inspect `i`, `numbers.length`, and `total`.

## ConditionalBreakpointDemo.java

```java
package com.example.debugging;

public class ConditionalBreakpointDemo {

    public static void main(String[] args) {
        for (int i = 1; i <= 10; i++) {
            System.out.println("Processing item: " + i);
        }
    }
}
```

Add breakpoint on print line. Right-click breakpoint and condition:

```java
i == 7
```

Debugger stops only when `i` is 7.

## Assignment

```text
1. Create DebugDemo
2. Add breakpoint
3. Debug program
4. Step Into calculateTotal
5. Step Out
6. Add Watch variables
7. Use Evaluate Expression
8. Create BugDemo
9. Debug the bug
10. Fix loop condition
11. Create ConditionalBreakpointDemo
12. Add conditional breakpoint i == 7
```

When done, reply:

```text
Module 6 completed
```
