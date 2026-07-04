# Module 09 — Git Inside IntelliJ IDEA

## Goal
Learn Git workflow inside IntelliJ IDEA.

You will practice enabling Git, initial commit, Git Log, branches, compare, merge, rollback, and conflict resolution.

## Enable Git

Use:

```text
VCS → Enable Version Control Integration → Git
```

## Initial Commit

Open Commit window:

| OS | Shortcut |
|---|---|
| Mac | `Cmd + 0` |
| Windows/Linux | `Alt + 0` |

Commit message:

```text
Initial IntelliJ learning project
```

## Git Log

Open:

| OS | Shortcut |
|---|---|
| Mac | `Cmd + 9` |
| Windows/Linux | `Alt + 9` |

Open Log tab.

## Create Branch

Create:

```text
feature/git-practice
```

## GitPracticeDemo.java

```java
package com.example.gitpractice;

public class GitPracticeDemo {

    public static void main(String[] args) {
        System.out.println("Practicing Git inside IntelliJ IDEA.");
    }
}
```

Commit:

```text
Add Git practice demo
```

## Compare and Merge

Use branch widget:

```text
main → Compare with Current
feature/git-practice → Merge into Current
```

## Rollback

Make temporary edit. In Commit window, right-click file:

```text
Rollback
```

## Conflict Practice

Create `ConflictDemo.java` on main:

```java
package com.example.gitpractice;

public class ConflictDemo {

    public String message() {
        return "Message from main branch";
    }
}
```

Commit. Create branch `feature/conflict-practice`, edit same line, commit. Return to main, edit same line differently, commit. Merge feature into main. Use IntelliJ merge viewer and choose final content:

```java
return "Resolved message from main and feature branch";
```

## Git Shortcuts

| Action | Mac | Windows/Linux |
|---|---|---|
| Commit window | `Cmd + 0` | `Alt + 0` |
| Git window | `Cmd + 9` | `Alt + 9` |
| Commit | `Cmd + K` | `Ctrl + K` |
| Push | `Cmd + Shift + K` | `Ctrl + Shift + K` |

## Assignment

```text
1. Enable Git
2. Make initial commit
3. Open Git Log
4. Create feature/git-practice branch
5. Create GitPracticeDemo
6. Commit it
7. Compare branch with main
8. Merge branch into main
9. Practice rollback
10. Create and resolve a conflict
```

When done, reply:

```text
Module 9 completed
```
