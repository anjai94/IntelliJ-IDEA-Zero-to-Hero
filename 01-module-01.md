# Module 01 — IntelliJ IDEA Setup and First Java Program

## Goal
Set up IntelliJ IDEA for Java development and run your first Java program. The focus is IntelliJ workflow, not Java theory.

You will learn how to open IntelliJ, create a Java project, select/configure JDK 21, understand the Project tool window, create packages/classes, run a Java class, read the Run output, and fix simple setup issues.

## Main IntelliJ Skills

| Skill | IntelliJ Area |
|---|---|
| Create project | File → New → Project |
| Configure JDK | Project Structure |
| Create class | Project window |
| Run program | Green Run icon / Run configuration |
| Read output | Run tool window |
| Reformat code | Editor action |

## Step 1 — Create Project

Open IntelliJ IDEA and choose:

```text
New Project
```

Choose Java and name the project:

```text
idea-zero-to-hero
```

Recommended location:

```text
~/IdeaProjects/idea-zero-to-hero
```

## Step 2 — Select JDK 21

In the New Project screen, set JDK to:

```text
JDK 21
```

If it is missing:

```text
Add JDK → Download JDK → Version 21
```

## Step 3 — Understand Project Window

Open Project window:

| OS | Shortcut |
|---|---|
| Mac | `Cmd + 1` |
| Windows/Linux | `Alt + 1` |

You should see:

```text
idea-zero-to-hero
 ├── .idea
 ├── src
 └── idea-zero-to-hero.iml
```

`src` is where source code goes. `.idea` contains IntelliJ project settings.

## Step 4 — Create Package

Right-click `src`:

```text
New → Package
```

Create:

```text
com.example.first
```

## Step 5 — Create Main Class

Right-click package:

```text
New → Java Class
```

Name:

```text
Main
```

Paste:

```java
package com.example.first;

public class Main {

    public static void main(String[] args) {
        System.out.println("Hello IntelliJ IDEA!");
        System.out.println("This is my first Java program in IntelliJ.");
    }
}
```

## Step 6 — Run

Click the green run icon beside `main()`, or right-click inside the file and choose Run, or use:

| OS | Shortcut |
|---|---|
| Mac | `Ctrl + R` |
| Windows/Linux | `Shift + F10` |

Expected output:

```text
Hello IntelliJ IDEA!
This is my first Java program in IntelliJ.
```

## Step 7 — Create AboutMe Class

Create class:

```text
AboutMe
```

Paste:

```java
package com.example.first;

public class AboutMe {

    public static void main(String[] args) {
        String name = "Nithakanan";
        String goal = "Learn IntelliJ IDEA properly";

        System.out.println("Name: " + name);
        System.out.println("Goal: " + goal);
    }
}
```

Expected output:

```text
Name: Nithakanan
Goal: Learn IntelliJ IDEA properly
```

## Step 8 — Reformat Code

| OS | Shortcut |
|---|---|
| Mac | `Cmd + Option + L` |
| Windows/Linux | `Ctrl + Alt + L` |

## Common Issues

### No Run Button
Check that the class has:

```java
public static void main(String[] args)
```

### Wrong JDK
Open:

```text
File → Project Structure → Project
```

Check SDK is JDK 21.

### Package Error
The first line must match the package location:

```java
package com.example.first;
```

## Assignment

```text
1. Create idea-zero-to-hero
2. Configure JDK 21
3. Create package com.example.first
4. Create Main class
5. Run Main
6. Create AboutMe class
7. Run AboutMe
8. Reformat both files
9. Open Project window with shortcut
10. Open Search Everywhere using Shift Shift
```

When done, reply:

```text
Module 1 completed
```
