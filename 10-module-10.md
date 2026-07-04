# Module 10 — Code Review Workflow

## Goal
Learn how to review code changes inside IntelliJ before committing.

You will practice feature branches, diffs, selected commits, changelists, shelve/unshelve, compare with main, rollback, and commit messages.

## Create Branch

```text
feature/code-review-practice
```

## ReviewDemo.java

```java
package com.example.codereview;

public class ReviewDemo {

    public static void main(String[] args) {
        System.out.println("Code review practice in IntelliJ IDEA.");
        printStatus("READY");
    }

    private static void printStatus(String status) {
        System.out.println("Status: " + status);
    }
}
```

## TemporaryDemo.java

```java
package com.example.codereview;

public class TemporaryDemo {

    public static void main(String[] args) {
        System.out.println("This is a temporary file.");
    }
}
```

Do not commit this if it is temporary.

## Review Diff

Open Commit window and click changed files.

Check for:

```text
Accidental files
Generated files
Debug prints
Secrets
Unrelated changes
Formatting issues
```

## Commit Selected File Only

Select only `ReviewDemo.java`.

Commit:

```text
Add code review practice demo
```

## Changelists

Create:

```text
Feature work
Temporary work
```

Move `TemporaryDemo.java` to Temporary work.

## Shelve and Unshelve

Right-click file/changelist:

```text
Shelve Changes
```

Later:

```text
Shelf → Unshelve
```

## Compare with Main

```text
Branch widget → main → Compare with Current
```

## Code Review Checklist

```text
1. Review every changed file
2. Remove unrelated files
3. Remove debug prints
4. Remove secrets
5. Exclude generated files
6. Reformat code
7. Write clear commit message
8. Run relevant tests
```

## Assignment

```text
1. Create feature/code-review-practice
2. Create ReviewDemo
3. Create TemporaryDemo
4. Review diff
5. Commit only ReviewDemo
6. Create changelist Temporary work
7. Move TemporaryDemo to changelist
8. Shelve TemporaryDemo
9. Unshelve it
10. Rollback TemporaryDemo
11. Compare branch with main
12. Review Git Log
```

When done, reply:

```text
Module 10 completed
```
