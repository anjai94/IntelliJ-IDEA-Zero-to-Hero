# IntelliJ IDEA Zero to Hero — FULL No-Removal Markdown Course

This package was regenerated because earlier files were too minimal.

This version includes:

- 26 detailed module Markdown files
- Step-by-step IntelliJ actions
- Java/Spring code for practice
- HTTP Client examples
- Maven, Gradle, Docker, database, debugging, security, plugin, AI, and capstone content
- Assignments and expected completion replies
- Combined full-course Markdown file
- Progress checklist
- File statistics

Generated: 2026-07-04T13:50:53


---

# IntelliJ IDEA Zero to Hero — Full No-Removal Course Index

This regenerated archive is expanded module-by-module and is not a summary-only version.

## Modules

- [Module 01 — IntelliJ IDEA Setup and First Java Program](01-module-01.md)
- [Module 02 — IntelliJ Navigation Basics](02-module-02.md)
- [Module 03 — Writing Code Faster](03-module-03.md)
- [Module 04 — Project Structure and Java Packages](04-module-04.md)
- [Module 05 — Running Applications and Run Configurations](05-module-05.md)
- [Module 06 — Debugging from Zero](06-module-06.md)
- [Module 07 — Maven in IntelliJ IDEA](07-module-07.md)
- [Module 08 — Gradle in IntelliJ IDEA](08-module-08.md)
- [Module 09 — Git Inside IntelliJ IDEA](09-module-09.md)
- [Module 10 — Code Review Workflow](10-module-10.md)
- [Module 11 — Unit Testing with JUnit](11-module-11.md)
- [Module 12 — Code Quality and Refactoring](12-module-12.md)
- [Module 13 — Spring Boot Project Setup](13-module-13.md)
- [Module 14 — REST API Development](14-module-14.md)
- [Module 15 — IntelliJ HTTP Client Deep Dive](15-module-15.md)
- [Module 16 — Database Integration](16-module-16.md)
- [Module 17 — Services Tool Window and Runtime Management](17-module-17.md)
- [Module 18 — Docker and Local Development](18-module-18.md)
- [Module 19 — Advanced Debugging](19-module-19.md)
- [Module 20 — IntelliJ Productivity Mastery](20-module-20.md)
- [Module 21 — Security-Focused IntelliJ Usage](21-module-21.md)
- [Module 22 — Plugin Ecosystem](22-module-22.md)
- [Module 23 — AI-Assisted Development](23-module-23.md)
- [Module 24 — Real-World Java/Spring Project Structure](24-module-24.md)
- [Module 25 — Working with Large Codebases](25-module-25.md)
- [Module 26 — Capstone Secure Task Manager API](26-module-26.md)


---

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


---

# Module 02 — IntelliJ Navigation Basics

## Goal
Learn how to move around a project quickly without manually clicking folders.

You will practice Search Everywhere, Go to Class, Go to File, Recent Files, Go to Declaration, Find Usages, Terminal, and navigation history.

## Create Practice Package

Create:

```text
com.example.navigation
```

Create classes:

```text
Customer
Order
Payment
NavigationApp
```

## Customer.java

```java
package com.example.navigation;

public class Customer {

    private String name;

    public Customer(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

## Order.java

```java
package com.example.navigation;

public class Order {

    private String itemName;
    private Customer customer;

    public Order(String itemName, Customer customer) {
        this.itemName = itemName;
        this.customer = customer;
    }

    public String getItemName() {
        return itemName;
    }

    public Customer getCustomer() {
        return customer;
    }
}
```

## Payment.java

```java
package com.example.navigation;

public class Payment {

    public void pay(Order order) {
        System.out.println("Paid for: " + order.getItemName());
        System.out.println("Customer: " + order.getCustomer().getName());
    }
}
```

## NavigationApp.java

```java
package com.example.navigation;

public class NavigationApp {

    public static void main(String[] args) {
        Customer customer = new Customer("Nithakanan");
        Order order = new Order("IntelliJ IDEA Course", customer);

        Payment payment = new Payment();
        payment.pay(order);
    }
}
```

Expected output:

```text
Paid for: IntelliJ IDEA Course
Customer: Nithakanan
```

## Search Everywhere

| OS | Shortcut |
|---|---|
| Mac | `Shift` `Shift` |
| Windows/Linux | `Shift` `Shift` |

Search and open:

```text
Customer
Order
Payment
NavigationApp
```

## Go to Class

| OS | Shortcut |
|---|---|
| Mac | `Cmd + O` |
| Windows/Linux | `Ctrl + N` |

Search `Payment`.

## Go to File

| OS | Shortcut |
|---|---|
| Mac | `Cmd + Shift + O` |
| Windows/Linux | `Ctrl + Shift + N` |

Search `NavigationApp.java`.

## Recent Files

| OS | Shortcut |
|---|---|
| Mac | `Cmd + E` |
| Windows/Linux | `Ctrl + E` |

Use this to switch between files instead of clicking tabs.

## Go to Declaration

In `NavigationApp.java`, use:

| OS | Shortcut |
|---|---|
| Mac | `Cmd + Click` |
| Windows/Linux | `Ctrl + Click` |

Click `Customer`, `Order`, `Payment`, and `pay`.

## Find Usages

| OS | Shortcut |
|---|---|
| Mac | `Option + F7` |
| Windows/Linux | `Alt + F7` |

Try on `Customer`, `Order`, `Payment.pay`, and `getName`.

## Back and Forward

| Action | Mac | Windows/Linux |
|---|---|---|
| Back | `Cmd + Option + Left` | `Ctrl + Alt + Left` |
| Forward | `Cmd + Option + Right` | `Ctrl + Alt + Right` |

## Terminal

| OS | Shortcut |
|---|---|
| Mac | `Option + F12` |
| Windows/Linux | `Alt + F12` |

Run:

```bash
pwd
ls
```

## Assignment

```text
1. Create com.example.navigation
2. Create Customer, Order, Payment, NavigationApp
3. Run NavigationApp
4. Open each class using Shift Shift
5. Open Customer using Go to Class
6. Open NavigationApp.java using Go to File
7. Use Recent Files
8. Use Go to Declaration
9. Use Find Usages on Customer
10. Open Terminal
```

When done, reply:

```text
Module 2 completed
```


---

# Module 03 — Writing Code Faster

## Goal
Learn IntelliJ features that help you write Java code faster and with fewer mistakes.

You will practice code completion, Generate constructor/getters/setters/toString, auto-import, reformat, duplicate/delete/move lines, live templates, postfix completion, and Quick Fix.

## Create Package

```text
com.example.fastcoding
```

Create:

```text
Product
Order
Payment
ShopApp
```

## Product.java

Start with fields:

```java
package com.example.fastcoding;

public class Product {

    private String name;
    private double price;
    private int quantity;

}
```

Use Generate Code:

| OS | Shortcut |
|---|---|
| Mac | `Cmd + N` |
| Windows/Linux | `Alt + Insert` |

Generate constructor, getters, setters, and `toString`.

Final version:

```java
package com.example.fastcoding;

public class Product {

    private String name;
    private double price;
    private int quantity;

    public Product(String name, double price, int quantity) {
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public int getQuantity() {
        return quantity;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }

    public double getTotalPrice() {
        return price * quantity;
    }

    @Override
    public String toString() {
        return "Product{name='" + name + "', price=" + price + ", quantity=" + quantity + "}";
    }
}
```

## Order.java

```java
package com.example.fastcoding;

public class Order {

    private Product product;
    private String customerName;

    public Order(Product product, String customerName) {
        this.product = product;
        this.customerName = customerName;
    }

    public void printSummary() {
        System.out.println("Customer: " + customerName);
        System.out.println("Product: " + product.getName());
        System.out.println("Total: " + product.getTotalPrice());
    }
}
```

## Payment.java

```java
package com.example.fastcoding;

public class Payment {

    public void processPayment(Order order) {
        System.out.println("Payment processed successfully.");
    }
}
```

## ShopApp.java

```java
package com.example.fastcoding;

public class ShopApp {

    public static void main(String[] args) {
        Product product = new Product("Laptop", 1200.00, 2);
        Order order = new Order(product, "Nithakanan");

        order.printSummary();

        Payment payment = new Payment();
        payment.processPayment(order);
    }
}
```

Expected output:

```text
Customer: Nithakanan
Product: Laptop
Total: 2400.0
Payment processed successfully.
```

## Shortcuts

| Action | Mac | Windows/Linux |
|---|---|---|
| Basic completion | `Ctrl + Space` | `Ctrl + Space` |
| Smart completion | `Ctrl + Shift + Space` | `Ctrl + Shift + Space` |
| Generate code | `Cmd + N` | `Alt + Insert` |
| Quick Fix | `Option + Enter` | `Alt + Enter` |
| Reformat | `Cmd + Option + L` | `Ctrl + Alt + L` |
| Optimize imports | `Ctrl + Option + O` | `Ctrl + Alt + O` |
| Line comment | `Cmd + /` | `Ctrl + /` |
| Duplicate line | `Cmd + D` | `Ctrl + D` |
| Delete line | `Cmd + Delete` | `Ctrl + Y` |

## Live Templates

```text
psvm → public static void main
sout → System.out.println
soutv → print variable
soutp → print parameters
soutm → print method
```

## Assignment

```text
1. Create com.example.fastcoding
2. Create Product, Order, Payment, ShopApp
3. Generate constructor/getters/setters/toString
4. Run ShopApp
5. Practice duplicate/delete/move line
6. Practice comments
7. Practice psvm and sout
8. Use Quick Fix 3 times
9. Reformat all files
10. Optimize imports
```

When done, reply:

```text
Module 3 completed
```


---

# Module 04 — Project Structure and Java Packages

## Goal
Understand packages, classes, and clean project structure in IntelliJ IDEA.

Important clarification:

```text
com.example.taskmanager.model.User
```

should not be created as one package. Correct approach:

```text
Package: com.example.taskmanager.model
Class: User
```

## Target Structure

```text
src
 └── com.example.taskmanager
     ├── model
     │   ├── Task.java
     │   └── User.java
     ├── service
     │   ├── TaskService.java
     │   └── UserService.java
     ├── controller
     │   ├── TaskController.java
     │   └── UserController.java
     ├── util
     │   └── TextUtil.java
     └── TaskManagerApp.java
```

## Create Packages

```text
com.example.taskmanager
com.example.taskmanager.model
com.example.taskmanager.service
com.example.taskmanager.controller
com.example.taskmanager.util
```

## Task.java

```java
package com.example.taskmanager.model;

public class Task {

    private String title;
    private boolean completed;

    public Task(String title) {
        this.title = title;
        this.completed = false;
    }

    public String getTitle() {
        return title;
    }

    public boolean isCompleted() {
        return completed;
    }

    public void markCompleted() {
        completed = true;
    }
}
```

## User.java

```java
package com.example.taskmanager.model;

public class User {

    private String name;

    public User(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

## TextUtil.java

```java
package com.example.taskmanager.util;

public class TextUtil {

    public static String uppercase(String value) {
        return value.toUpperCase();
    }
}
```

## TaskService.java

```java
package com.example.taskmanager.service;

import com.example.taskmanager.model.Task;

public class TaskService {

    public Task createTask(String title) {
        return new Task(title);
    }

    public void completeTask(Task task) {
        task.markCompleted();
    }
}
```

## UserService.java

```java
package com.example.taskmanager.service;

import com.example.taskmanager.model.User;

public class UserService {

    public User createUser(String name) {
        return new User(name);
    }
}
```

## TaskController.java

```java
package com.example.taskmanager.controller;

import com.example.taskmanager.model.Task;
import com.example.taskmanager.service.TaskService;
import com.example.taskmanager.util.TextUtil;

public class TaskController {

    private final TaskService taskService = new TaskService();

    public Task createTask(String title) {
        return taskService.createTask(TextUtil.uppercase(title));
    }

    public void completeTask(Task task) {
        taskService.completeTask(task);
    }
}
```

## UserController.java

```java
package com.example.taskmanager.controller;

import com.example.taskmanager.model.User;
import com.example.taskmanager.service.UserService;

public class UserController {

    private final UserService userService = new UserService();

    public User createUser(String name) {
        return userService.createUser(name);
    }
}
```

## TaskManagerApp.java

```java
package com.example.taskmanager;

import com.example.taskmanager.controller.TaskController;
import com.example.taskmanager.controller.UserController;
import com.example.taskmanager.model.Task;
import com.example.taskmanager.model.User;

public class TaskManagerApp {

    public static void main(String[] args) {
        UserController userController = new UserController();
        TaskController taskController = new TaskController();

        User user = userController.createUser("Nithakanan");
        Task task = taskController.createTask("Learn IntelliJ packages");

        System.out.println("User: " + user.getName());
        System.out.println("Task: " + task.getTitle());
        System.out.println("Completed: " + task.isCompleted());

        taskController.completeTask(task);

        System.out.println("Completed after update: " + task.isCompleted());
    }
}
```

Expected:

```text
User: Nithakanan
Task: LEARN INTELLIJ PACKAGES
Completed: false
Completed after update: true
```

## IntelliJ Skills

```text
Create Package
Create Java Class
Move Class with F6
Rename with Shift + F6
Find Usages with Option/Alt + F7
Reformat Code
Optimize Imports
```

## Assignment

```text
1. Create full package structure
2. Create all model/service/controller/util classes
3. Run TaskManagerApp
4. Use Find Usages on User
5. Use Find Usages on TaskService
6. Rename TextUtil.uppercase using Shift + F6
7. Rename it back if needed
8. Reformat all files
```

When done, reply:

```text
Module 4 completed
```


---

# Module 05 — Running Applications and Run Configurations

## Goal
Learn how IntelliJ runs applications and how to configure run behavior.

You will practice running classes, editing run configurations, passing program arguments, passing environment variables, creating dev/prod-like configurations, and understanding Run output.

## Package

```text
com.example.runconfig
```

Create:

```text
RunDemo
ArgumentDemo
EnvironmentDemo
```

## RunDemo.java

```java
package com.example.runconfig;

public class RunDemo {

    public static void main(String[] args) {
        System.out.println("Application is running from IntelliJ IDEA.");
    }
}
```

## ArgumentDemo.java

```java
package com.example.runconfig;

public class ArgumentDemo {

    public static void main(String[] args) {
        System.out.println("Number of arguments: " + args.length);

        for (String arg : args) {
            System.out.println("Argument: " + arg);
        }
    }
}
```

Run without arguments. Then open:

```text
Run → Edit Configurations
```

Set Program arguments:

```text
dev 8080 enabled
```

Expected:

```text
Number of arguments: 3
Argument: dev
Argument: 8080
Argument: enabled
```

## EnvironmentDemo.java

```java
package com.example.runconfig;

public class EnvironmentDemo {

    public static void main(String[] args) {
        String appMode = System.getenv("APP_MODE");
        String appUser = System.getenv("APP_USER");

        System.out.println("APP_MODE = " + appMode);
        System.out.println("APP_USER = " + appUser);
    }
}
```

Set environment variables:

```text
APP_MODE=local;APP_USER=Nithakanan
```

Expected:

```text
APP_MODE = local
APP_USER = Nithakanan
```

## Create Multiple Configurations

Local:

```text
EnvironmentDemo - Local
APP_MODE=local;APP_USER=Nithakanan
```

Production simulation:

```text
EnvironmentDemo - Prod Simulation
APP_MODE=prod;APP_USER=prod-user
```

Never use real production secrets in local run configurations.

## Important Fields

```text
Main class
Program arguments
Environment variables
Working directory
JDK
Module classpath
```

## Shortcuts

| Action | Mac | Windows/Linux |
|---|---|---|
| Run | `Ctrl + R` | `Shift + F10` |
| Debug | `Ctrl + D` | `Shift + F9` |
| Stop | `Cmd + F2` | `Ctrl + F2` |
| Terminal | `Option + F12` | `Alt + F12` |

## Assignment

```text
1. Create RunDemo and run it
2. Create ArgumentDemo
3. Run without arguments
4. Add program arguments
5. Create EnvironmentDemo
6. Add APP_MODE and APP_USER env vars
7. Create Local and Prod Simulation configurations
8. Rename one run configuration
9. Duplicate one run configuration
```

When done, reply:

```text
Module 5 completed
```


---

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


---

# Module 07 — Maven in IntelliJ IDEA

## Goal
Learn how to use Maven inside IntelliJ IDEA.

You will practice creating Maven project, understanding `pom.xml`, running lifecycle goals, adding dependencies, reloading Maven, and using external libraries.

## Create Maven Project

Create:

```text
maven-practice
```

Use:

```text
Maven
Java 21
Package: com.example.mavenpractice
```

## Structure

```text
maven-practice
 ├── pom.xml
 └── src
     ├── main/java
     └── test/java
```

## MavenDemo.java

```java
package com.example.mavenpractice;

public class MavenDemo {

    public static void main(String[] args) {
        System.out.println("Maven project is running in IntelliJ IDEA.");
    }
}
```

## Maven Tool Window

Open:

```text
View → Tool Windows → Maven
```

Lifecycle goals:

```text
clean
compile
test
package
install
```

Run clean, compile, package.

## Add Dependency

In `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.14.0</version>
</dependency>
```

Click Load Maven Changes.

## StringCheckDemo.java

```java
package com.example.mavenpractice;

import org.apache.commons.lang3.StringUtils;

public class StringCheckDemo {

    public static void main(String[] args) {
        String value = "   ";

        if (StringUtils.isBlank(value)) {
            System.out.println("Value is blank");
        } else {
            System.out.println("Value is not blank");
        }
    }
}
```

Expected:

```text
Value is blank
```

## Maven Commands

```bash
mvn clean compile
mvn test
mvn package
mvn -U clean package
```

`-U` forces Maven to retry dependency downloads.

## Assignment

```text
1. Create maven-practice
2. Create MavenDemo
3. Run MavenDemo
4. Open Maven tool window
5. Run clean, compile, package
6. Add commons-lang3
7. Reload Maven
8. Create StringCheckDemo
9. Run StringCheckDemo
10. Check External Libraries
```

When done, reply:

```text
Module 7 completed
```


---

# Module 08 — Gradle in IntelliJ IDEA

## Goal
Learn how to use Gradle inside IntelliJ IDEA.

You will practice creating Gradle project, understanding `build.gradle`, running tasks, adding dependencies, reloading Gradle, and using Gradle wrapper.

## Create Gradle Project

Create:

```text
gradle-practice
```

Use:

```text
Gradle
Java
JDK 21
Package: com.example.gradlepractice
```

## Structure

```text
gradle-practice
 ├── build.gradle
 ├── settings.gradle
 ├── gradlew
 ├── gradlew.bat
 └── src/main/java
```

## GradleDemo.java

```java
package com.example.gradlepractice;

public class GradleDemo {

    public static void main(String[] args) {
        System.out.println("Gradle project is running in IntelliJ IDEA.");
    }
}
```

## Gradle Tool Window

Open:

```text
View → Tool Windows → Gradle
```

Run tasks:

```text
clean
build
test
jar
```

## Add Dependency

In `build.gradle`:

```groovy
dependencies {
    implementation 'org.apache.commons:commons-lang3:3.14.0'
    testImplementation platform('org.junit:junit-bom:5.10.0')
    testImplementation 'org.junit.jupiter:junit-jupiter'
}
```

Reload Gradle.

## GradleStringCheckDemo.java

```java
package com.example.gradlepractice;

import org.apache.commons.lang3.StringUtils;

public class GradleStringCheckDemo {

    public static void main(String[] args) {
        String value = "";

        if (StringUtils.isBlank(value)) {
            System.out.println("Blank value detected from Gradle project.");
        }
    }
}
```

## Gradle Wrapper

Mac/Linux:

```bash
./gradlew clean build
```

Windows:

```bash
gradlew.bat clean build
```

Wrapper keeps Gradle version consistent across machines.

## Assignment

```text
1. Create gradle-practice
2. Create GradleDemo
3. Run GradleDemo
4. Open Gradle tool window
5. Run clean and build
6. Add commons-lang3
7. Reload Gradle
8. Create GradleStringCheckDemo
9. Run it
10. Run ./gradlew clean build
```

When done, reply:

```text
Module 8 completed
```


---

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


---

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


---

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


---

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


---

# Module 13 — Spring Boot Project Setup

## Goal
Create and run a Spring Boot project from IntelliJ IDEA.

You will practice Spring project creation, dependency selection, main class, running Spring Boot, creating a controller, editing `application.properties`, changing port, and reading logs.

## Create Project

Create:

```text
springboot-practice
```

Use:

```text
Spring Boot
Maven
Java 21
Group: com.example
Artifact: springboot-practice
Dependency: Spring Web
```

## Main Class

```java
package com.example.springbootpractice;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringbootPracticeApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootPracticeApplication.class, args);
    }
}
```

Run it. Expected logs:

```text
Tomcat started on port 8080
Started SpringbootPracticeApplication
```

## HelloController.java

Create package:

```text
com.example.springbootpractice.controller
```

Create:

```java
package com.example.springbootpractice.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello from Spring Boot and IntelliJ IDEA";
    }

    @GetMapping("/greet")
    public String greet() {
        return "Welcome to the IntelliJ Spring Boot module";
    }
}
```

Open:

```text
http://localhost:8080/hello
http://localhost:8080/greet
```

## Run Configuration

Rename configuration:

```text
Spring Boot Practice - Local
```

Check:

```text
Main class
Module
JDK
Environment variables
Program arguments
```

## Change Port

In `application.properties`:

```properties
server.port=8081
```

Restart and test:

```text
http://localhost:8081/hello
```

Change back:

```properties
server.port=8080
```

## Common Issues

```text
Port already in use → stop old app or change port
Whitelabel Error Page → URL has no matching endpoint
Controller not found → package must be under root package
```

## Assignment

```text
1. Create springboot-practice
2. Add Spring Web
3. Run main class
4. Create controller package
5. Create HelloController
6. Test /hello
7. Test /greet
8. Rename run configuration
9. Change port to 8081
10. Test again
11. Change port back to 8080
12. Review logs
```

When done, reply:

```text
Module 13 completed
```


---

# Module 14 — REST API Development

## Goal
Build a simple Task REST API and test it from IntelliJ.

You will practice model/service/controller packages, GET/POST/PUT/DELETE endpoints, in-memory logic, HTTP Client `.http` file, and debugging request flow.

## Target Structure

```text
com.example.springbootpractice
 ├── controller/TaskController.java
 ├── model/Task.java
 └── service/TaskService.java
```

## Task.java

```java
package com.example.springbootpractice.model;

public class Task {

    private Long id;
    private String title;
    private String status;

    public Task() {
    }

    public Task(Long id, String title, String status) {
        this.id = id;
        this.title = title;
        this.status = status;
    }

    public Long getId() { return id; }
    public String getTitle() { return title; }
    public String getStatus() { return status; }
    public void setId(Long id) { this.id = id; }
    public void setTitle(String title) { this.title = title; }
    public void setStatus(String status) { this.status = status; }
}
```

## TaskService.java

```java
package com.example.springbootpractice.service;

import com.example.springbootpractice.model.Task;
import org.springframework.stereotype.Service;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

@Service
public class TaskService {

    private final List<Task> tasks = new ArrayList<>();
    private long nextId = 1;

    public TaskService() {
        tasks.add(new Task(nextId++, "Learn IntelliJ REST API workflow", "OPEN"));
        tasks.add(new Task(nextId++, "Test API using HTTP Client", "IN_PROGRESS"));
    }

    public List<Task> getAllTasks() {
        return tasks;
    }

    public Optional<Task> getTaskById(Long id) {
        return tasks.stream().filter(task -> task.getId().equals(id)).findFirst();
    }

    public Task createTask(Task task) {
        task.setId(nextId++);
        if (task.getStatus() == null || task.getStatus().isBlank()) {
            task.setStatus("OPEN");
        }
        tasks.add(task);
        return task;
    }

    public Optional<Task> updateTask(Long id, Task updatedTask) {
        return getTaskById(id).map(existingTask -> {
            existingTask.setTitle(updatedTask.getTitle());
            existingTask.setStatus(updatedTask.getStatus());
            return existingTask;
        });
    }

    public boolean deleteTask(Long id) {
        return tasks.removeIf(task -> task.getId().equals(id));
    }
}
```

## TaskController.java

```java
package com.example.springbootpractice.controller;

import com.example.springbootpractice.model.Task;
import com.example.springbootpractice.service.TaskService;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/tasks")
public class TaskController {

    private final TaskService taskService;

    public TaskController(TaskService taskService) {
        this.taskService = taskService;
    }

    @GetMapping
    public List<Task> getAllTasks() {
        return taskService.getAllTasks();
    }

    @GetMapping("/{id}")
    public ResponseEntity<Task> getTaskById(@PathVariable Long id) {
        return taskService.getTaskById(id)
                .map(ResponseEntity::ok)
                .orElse(ResponseEntity.notFound().build());
    }

    @PostMapping
    public Task createTask(@RequestBody Task task) {
        return taskService.createTask(task);
    }

    @PutMapping("/{id}")
    public ResponseEntity<Task> updateTask(@PathVariable Long id, @RequestBody Task task) {
        return taskService.updateTask(id, task)
                .map(ResponseEntity::ok)
                .orElse(ResponseEntity.notFound().build());
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteTask(@PathVariable Long id) {
        boolean deleted = taskService.deleteTask(id);
        return deleted ? ResponseEntity.noContent().build() : ResponseEntity.notFound().build();
    }
}
```

## HTTP Client File

Create:

```text
src/test/http/task-api.http
```

```http
### Get all tasks
GET http://localhost:8080/tasks

### Get task by id
GET http://localhost:8080/tasks/1

### Create task
POST http://localhost:8080/tasks
Content-Type: application/json

{
  "title": "Practice REST API development",
  "status": "OPEN"
}

### Update task
PUT http://localhost:8080/tasks/1
Content-Type: application/json

{
  "title": "Updated task title",
  "status": "COMPLETED"
}

### Delete task
DELETE http://localhost:8080/tasks/1
```

## Debug Request Flow

Add breakpoints in:

```text
TaskController.createTask
TaskService.createTask
```

Debug app and run POST request.

## Assignment

```text
1. Create model/service/controller packages
2. Create Task
3. Create TaskService
4. Create TaskController
5. Run Spring Boot app
6. Test GET /tasks
7. Create task-api.http
8. Test GET/POST/PUT/DELETE
9. Debug POST request
10. Review Controller → Service flow
```

When done, reply:

```text
Module 14 completed
```


---

# Module 15 — IntelliJ HTTP Client Deep Dive

## Goal
Use IntelliJ HTTP Client like a repeatable API testing tool.

You will practice `.http` files, request names, environments, private environment files, CRUD organization, response validation scripts, cURL conversion, request generation, request history, and Git-safe setup.

## Advanced HTTP File

Create:

```text
src/test/http/task-api-advanced.http
```

## Environment File

Create:

```text
src/test/http/http-client.env.json
```

```json
{
  "local": {
    "baseUrl": "http://localhost:8080",
    "taskId": "1"
  },
  "local8081": {
    "baseUrl": "http://localhost:8081",
    "taskId": "1"
  }
}
```

## Private Environment File

Create:

```text
src/test/http/http-client.private.env.json
```

Example:

```json
{
  "local": {
    "token": "do-not-commit-real-token"
  }
}
```

Add to `.gitignore`:

```gitignore
http-client.private.env.json
**/http-client.private.env.json
```

## Full CRUD Requests

```http
### Get all tasks
# @name getAllTasks
GET {{baseUrl}}/tasks

### Get task by ID
# @name getTaskById
GET {{baseUrl}}/tasks/{{taskId}}

### Create task
# @name createTask
POST {{baseUrl}}/tasks
Content-Type: application/json

{
  "title": "Created from IntelliJ HTTP Client",
  "status": "OPEN"
}

### Update task
# @name updateTask
PUT {{baseUrl}}/tasks/{{taskId}}
Content-Type: application/json

{
  "title": "Updated from IntelliJ HTTP Client",
  "status": "COMPLETED"
}

### Delete task
# @name deleteTask
DELETE {{baseUrl}}/tasks/{{taskId}}
```

## Response Validation

```http
> {%
    client.test("Status is 200", function () {
        client.assert(response.status === 200, "Expected status 200");
    });
%}
```

## Invalid Request Example

```http
### Create invalid task
# @name createInvalidTask
POST {{baseUrl}}/tasks
Content-Type: application/json

{
  "title": "",
  "status": "OPEN"
}

> {%
    client.test("Invalid task behavior reviewed", function () {
        client.assert(response.status === 400 || response.status === 200, "Review validation behavior");
    });
%}
```

## cURL Conversion

Paste cURL:

```bash
curl -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"From curl","status":"OPEN"}'
```

IntelliJ can convert/suggest HTTP format.

## Request History

Use Find Action:

```text
HTTP Requests
HTTP Client
Show HTTP Requests
```

## Assignment

```text
1. Create task-api-advanced.http
2. Create http-client.env.json
3. Create private env file
4. Add private env to .gitignore
5. Add GET/POST/PUT/DELETE requests
6. Use {{baseUrl}} and {{taskId}}
7. Add validation script
8. Run all requests
9. Try cURL conversion
10. Try request generation from controller
11. Review request history
12. Commit only safe files
```

When done, reply:

```text
Module 15 completed
```


---

# Module 16 — Database Integration

## Goal
Connect Spring Boot Task API to a database and use IntelliJ database tools.

You will practice adding JPA/H2 dependencies, configuring H2, converting `Task` to entity, creating repository, replacing in-memory service, adding sample data, using H2 console, using Database tool window, and running SQL.

## Dependencies

Add to `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

For Spring Boot 4.x H2 browser console, you may also need:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-h2console</artifactId>
</dependency>
```

Reload Maven. If dependency transfer failure is cached:

```bash
mvn -U clean package
```

`-U` forces Maven to retry downloads.

## application.properties

```properties
spring.application.name=springboot-practice

spring.datasource.url=jdbc:h2:mem:taskdb
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

spring.h2.console.enabled=true
spring.h2.console.path=/h2-console

server.port=8080
```

## Task.java as JPA Entity

```java
package com.example.springbootpractice.model;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;

@Entity
public class Task {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;
    private String status;

    public Task() {
    }

    public Task(String title, String status) {
        this.title = title;
        this.status = status;
    }

    public Task(Long id, String title, String status) {
        this.id = id;
        this.title = title;
        this.status = status;
    }

    public Long getId() { return id; }
    public String getTitle() { return title; }
    public String getStatus() { return status; }
    public void setId(Long id) { this.id = id; }
    public void setTitle(String title) { this.title = title; }
    public void setStatus(String status) { this.status = status; }
}
```

## TaskRepository.java

```java
package com.example.springbootpractice.repository;

import com.example.springbootpractice.model.Task;
import org.springframework.data.jpa.repository.JpaRepository;

public interface TaskRepository extends JpaRepository<Task, Long> {
}
```

## TaskService.java Repository Version

```java
package com.example.springbootpractice.service;

import com.example.springbootpractice.model.Task;
import com.example.springbootpractice.repository.TaskRepository;
import org.springframework.stereotype.Service;

import java.util.List;
import java.util.Optional;

@Service
public class TaskService {

    private static final String DEFAULT_STATUS = "OPEN";
    private final TaskRepository taskRepository;

    public TaskService(TaskRepository taskRepository) {
        this.taskRepository = taskRepository;
    }

    public List<Task> getAllTasks() {
        return taskRepository.findAll();
    }

    public Optional<Task> getTaskById(Long id) {
        return taskRepository.findById(id);
    }

    public Task createTask(Task task) {
        if (task.getStatus() == null || task.getStatus().isBlank()) {
            task.setStatus(DEFAULT_STATUS);
        }
        return taskRepository.save(task);
    }

    public Optional<Task> updateTask(Long id, Task updatedTask) {
        return taskRepository.findById(id).map(existingTask -> {
            existingTask.setTitle(updatedTask.getTitle());
            existingTask.setStatus(updatedTask.getStatus() == null || updatedTask.getStatus().isBlank()
                    ? DEFAULT_STATUS
                    : updatedTask.getStatus());
            return taskRepository.save(existingTask);
        });
    }

    public boolean deleteTask(Long id) {
        if (!taskRepository.existsById(id)) {
            return false;
        }
        taskRepository.deleteById(id);
        return true;
    }
}
```

## DataInitializer.java

```java
package com.example.springbootpractice.config;

import com.example.springbootpractice.model.Task;
import com.example.springbootpractice.repository.TaskRepository;
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

@Component
public class DataInitializer implements CommandLineRunner {

    private final TaskRepository taskRepository;

    public DataInitializer(TaskRepository taskRepository) {
        this.taskRepository = taskRepository;
    }

    @Override
    public void run(String... args) {
        if (taskRepository.count() == 0) {
            taskRepository.save(new Task("Learn IntelliJ database workflow", "OPEN"));
            taskRepository.save(new Task("Connect Spring Boot with H2 database", "IN_PROGRESS"));
        }
    }
}
```

## H2 Console

Open:

```text
http://localhost:8080/h2-console
```

Login:

```text
JDBC URL: jdbc:h2:mem:taskdb
User Name: sa
Password: empty
```

If you get Whitelabel Error Page:

```text
1. Check spring.h2.console.enabled=true
2. Check /h2-console path
3. Add spring-boot-h2console for Spring Boot 4.x
4. Reload Maven with -U
5. Restart app
```

Your log proving DB works looks like:

```text
Database JDBC URL [jdbc:h2:mem:taskdb]
Hibernate: create table task
Hibernate: insert into task
```

## IntelliJ Database Tool Window

Open:

```text
View → Tool Windows → Database
+ → Data Source → H2
```

Use:

```text
JDBC URL: jdbc:h2:mem:taskdb
User: sa
Password: empty
```

Run SQL:

```sql
SELECT * FROM task;
```

## Assignment

```text
1. Add JPA and H2 dependencies
2. Reload Maven
3. Configure application.properties
4. Convert Task to JPA entity
5. Create TaskRepository
6. Replace TaskService
7. Create DataInitializer
8. Run app
9. Confirm Hibernate creates task table
10. Test GET /tasks
11. Open H2 console
12. Login with jdbc:h2:mem:taskdb
13. Run SELECT * FROM task
14. Open IntelliJ Database tool window
15. Try connecting to H2
16. Run SQL query
17. Test POST and confirm DB changes
```

When done, reply:

```text
Module 16 completed
```


---

# Module 17 — Services Tool Window and Runtime Management

## Goal
Use IntelliJ Services tool window to manage running applications, databases, Docker containers, and multiple run configurations.

## Open Services

```text
View → Tool Windows → Services
```

Shortcut is keymap dependent, often:

```text
Alt + 8
```

## Add Spring Boot Run Configuration

Run your Spring Boot app once. It should appear in Services.

If not:

```text
Services → + → Run Configuration Type → Application/Spring Boot
```

## Practice Controls

From Services, practice:

```text
Run
Stop
Rerun
Debug
Open console
Clear console
Scroll logs
```

## Multiple Configurations

Create two run configs:

```text
Spring Boot Practice - 8080
Program args: --server.port=8080
```

```text
Spring Boot Practice - 8081
Program args: --server.port=8081
```

Test:

```text
http://localhost:8080/tasks
http://localhost:8081/tasks
```

## Debug from Services

Add breakpoint:

```text
TaskController.getAllTasks
TaskService.getAllTasks
```

Click Debug in Services and run:

```http
GET http://localhost:8080/tasks
```

## Logs

Review:

```text
Startup logs
Tomcat port
Hibernate SQL
Errors
Stack traces
Request logs
```

## Services Can Show

```text
Spring Boot apps
Docker containers
Docker Compose services
Database connections
Application run configs
Gradle/Maven tasks
```

## Assignment

```text
1. Open Services
2. Run Spring Boot app from Services
3. Stop app
4. Rerun app
5. Debug app
6. Add breakpoint in TaskController
7. Run HTTP request and hit breakpoint
8. Create 8080 config
9. Create 8081 config
10. Run both if possible
11. Review logs
12. Stop all running apps
```

When done, reply:

```text
Module 17 completed
```


---

# Module 18 — Docker and Local Development

## Goal
Use Docker with IntelliJ to run PostgreSQL locally and connect Spring Boot to it.

You will practice Docker plugin/connection, `docker-compose.yml`, containers in Services, PostgreSQL dependency, datasource config, Database tool window, SQL verification, and secret safety.

## Check Docker

Make sure Docker Desktop is running.

IntelliJ:

```text
Settings → Build, Execution, Deployment → Docker
```

## docker-compose.yml

Create at project root:

```yaml
services:
  postgres:
    image: postgres:16
    container_name: task-postgres
    environment:
      POSTGRES_DB: taskdb
      POSTGRES_USER: taskuser
      POSTGRES_PASSWORD: taskpass
    ports:
      - "5432:5432"
    volumes:
      - task-postgres-data:/var/lib/postgresql/data

volumes:
  task-postgres-data:
```

## Start Container

From IntelliJ gutter or terminal:

```bash
docker compose up -d
docker ps
```

## Add PostgreSQL Dependency

```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
</dependency>
```

Reload Maven.

## application.properties for PostgreSQL

```properties
spring.application.name=springboot-practice

spring.datasource.url=jdbc:postgresql://localhost:5432/taskdb
spring.datasource.username=taskuser
spring.datasource.password=taskpass
spring.datasource.driver-class-name=org.postgresql.Driver

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

server.port=8080
```

Run app. Expected JDBC URL should show PostgreSQL.

## Test API

```http
GET http://localhost:8080/tasks
```

```http
POST http://localhost:8080/tasks
Content-Type: application/json

{
  "title": "Stored in PostgreSQL",
  "status": "OPEN"
}
```

## Database Tool Window

```text
View → Tool Windows → Database
+ → Data Source → PostgreSQL
```

Use:

```text
Host: localhost
Port: 5432
Database: taskdb
User: taskuser
Password: taskpass
```

SQL:

```sql
SELECT * FROM task;
```

## Stop Containers

Keep data:

```bash
docker compose down
```

Delete data:

```bash
docker compose down -v
```

## Security Habit

Learning credentials are okay for local practice. Real project credentials must not be committed.

## Assignment

```text
1. Verify Docker Desktop
2. Configure Docker in IntelliJ
3. Create docker-compose.yml
4. Start PostgreSQL
5. Add PostgreSQL dependency
6. Reload Maven
7. Configure application.properties
8. Run Spring Boot
9. Test GET/POST
10. Add PostgreSQL datasource in IntelliJ
11. Run SELECT * FROM task
12. Stop/start container and verify data persists
```

When done, reply:

```text
Module 18 completed
```


---

# Module 19 — Advanced Debugging

## Goal
Learn advanced debugging features in IntelliJ for Spring Boot applications.

You will practice debugging HTTP requests, stepping from controller to service, conditional breakpoints, logpoints, exception breakpoints, Evaluate Expression, Watches, Frames/call stack, Threads, method breakpoints, and remote debugging concept.

## Debug POST /tasks

Add breakpoints:

```text
TaskController.createTask
TaskService.createTask
```

Start app in Debug mode and run:

```http
POST http://localhost:8080/tasks
Content-Type: application/json

{
  "title": "Debug advanced POST",
  "status": "OPEN"
}
```

Inspect:

```text
request
task
createdTask
title
status
```

## Step Into Service

On:

```java
Task createdTask = taskService.createTask(task);
```

Press:

```text
F7
```

Use `F8` Step Over and `Shift + F8` Step Out.

## Conditional Breakpoint

In `getTaskById`, add condition:

```java
id == 999
```

Run:

```http
GET http://localhost:8080/tasks/999
```

## Logpoint

Right-click a breakpoint in `TaskService.createTask`:

```text
Log message to console
Do not suspend
```

Message:

```text
Creating task with title = {task.getTitle()}
```

## DebugErrorController.java

```java
package com.example.springbootpractice.debug;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class DebugErrorController {

    @GetMapping("/debug/error")
    public String error() {
        String value = null;
        return value.toUpperCase();
    }
}
```

Run:

```http
GET http://localhost:8080/debug/error
```

## Exception Breakpoint

Open breakpoints:

```text
Cmd + Shift + F8 / Ctrl + Shift + F8
```

Add Java Exception Breakpoint:

```text
NullPointerException
```

## Evaluate Expression

```text
Option + F8 / Alt + F8
```

Evaluate:

```java
task.getTitle()
task.getStatus()
id
```

## Frames and Threads

Focus on your package first:

```text
com.example.springbootpractice
```

Requests usually run on threads like:

```text
nio-8080-exec-1
```

## Remote Debugging Concept

A JVM can be started with:

```text
-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005
```

Then IntelliJ can attach to it.

## Assignment

```text
1. Debug POST /tasks
2. Step from controller to service
3. Inspect variables
4. Add conditional breakpoint id == 999
5. Test GET /tasks/999
6. Add logpoint in createTask
7. Confirm logpoint logs without stopping
8. Create DebugErrorController
9. Add NullPointerException breakpoint
10. Debug /debug/error
11. Use Evaluate Expression
12. Add Watches
13. Review Frames/call stack
14. Remove unnecessary breakpoints
```

When done, reply:

```text
Module 19 completed
```


---

# Module 20 — IntelliJ Productivity Mastery

## Goal
Master daily productivity tools in IntelliJ IDEA.

You will practice Search Everywhere, Find Action, Recent Files, File Structure, Bookmarks, TODO tracking, Scratch files, Local History, Live Templates, Postfix completion, Quick Fix, Structural Search, Replace in Path, and keyboard-only workflow.

## Search Everywhere

Shortcut:

```text
Shift Shift
```

Open:

```text
TaskController
TaskService
TaskRepository
application.properties
pom.xml
docker-compose.yml
```

## Find Action

| OS | Shortcut |
|---|---|
| Mac | `Cmd + Shift + A` |
| Windows/Linux | `Ctrl + Shift + A` |

Search:

```text
Reformat Code
Optimize Imports
Inspect Code
Search Structurally
Invalidate Caches
Edit Configurations
```

## Recent Files

| OS | Shortcut |
|---|---|
| Mac | `Cmd + E` |
| Windows/Linux | `Ctrl + E` |

## File Structure

| OS | Shortcut |
|---|---|
| Mac | `Cmd + F12` |
| Windows/Linux | `Ctrl + F12` |

Open `TaskController` and jump to methods.

## Bookmarks

Use Find Action:

```text
Toggle Bookmark
Show Bookmarks
```

Bookmark important files.

## TODO Tracking

Add:

```java
// TODO: Add authentication later
// TODO: Add pagination later
```

Open TODO tool window.

## Scratch Files

Use:

```text
Find Action → New Scratch File
```

Use for SQL notes, JSON samples, temporary Java snippets, HTTP payload drafts.

## Local History

Right-click file:

```text
Local History → Show History
```

Practice restore/compare.

## Live Templates

```text
psvm
sout
soutv
soutp
fori
itar
```

## Postfix Completion

Examples:

```text
name.sout
active.if
task.notnull
```

## Structural Search

Open:

```text
Find Action → Search Structurally
```

Search:

```java
System.out.println($TEXT$);
```

## Replace in Path

| OS | Shortcut |
|---|---|
| Mac | `Cmd + Shift + R` |
| Windows/Linux | `Ctrl + Shift + R` |

Always preview changes.

## Keyboard-Only Challenge

```text
1. Open TaskController using Shift Shift
2. Open File Structure
3. Jump to createTask
4. Go to declaration of TaskService
5. Find usages of createTask
6. Open Recent Files
7. Open HTTP file
8. Run request
9. Open Commit window
10. Review diff
```

## Assignment

```text
1. Use Search Everywhere 10 times
2. Use Find Action 5 times
3. Use Recent Files
4. Use File Structure
5. Add and view TODOs
6. Create Scratch File
7. Use Local History
8. Practice live templates
9. Practice postfix completion
10. Use Structural Search
11. Use Replace in Path safely
12. Complete keyboard-only challenge
```

When done, reply:

```text
Module 20 completed
```


---

# Module 21 — Security-Focused IntelliJ Usage

## Goal
Use IntelliJ IDEA for practical security-focused development and review.

You will practice finding hardcoded secrets, inspections, Structural Search, unsafe logging, vulnerable dependencies, basic validation, global error handling, security review notes, `.gitignore`, Inspect Code, and Git diff review.

## Use Project

```text
springboot-practice
```

## Practice 1 — Hardcoded Secret Detection

Create package:

```text
com.example.springbootpractice.securityreview
```

Create `SecretDemo`:

```java
package com.example.springbootpractice.securityreview;

public class SecretDemo {

    private static final String DB_PASSWORD = "admin123";
    private static final String API_TOKEN = "abc123-secret-token";

    public void connect() {
        System.out.println("Connecting with password: " + DB_PASSWORD);
        System.out.println("Using token: " + API_TOKEN);
    }
}
```

This is intentionally unsafe.

Open:

```text
Settings → Editor → Inspections
```

Search:

```text
Hardcoded
Password
```

## Replace with Safer Version

```java
package com.example.springbootpractice.securityreview;

public class SecretDemo {

    private static final String DB_PASSWORD_ENV = "DB_PASSWORD";
    private static final String API_TOKEN_ENV = "API_TOKEN";

    public void connect() {
        String dbPassword = System.getenv(DB_PASSWORD_ENV);
        String apiToken = System.getenv(API_TOKEN_ENV);

        if (dbPassword == null || apiToken == null) {
            throw new IllegalStateException("Required environment variables are missing");
        }

        System.out.println("Connecting with environment-based credentials");
    }
}
```

Rules:

```text
Do not print secrets
Do not commit real passwords
Use environment variables or secret manager
```

## Practice 2 — Unsafe Logging

Create `UnsafeLoggingDemo`:

```java
package com.example.springbootpractice.securityreview;

public class UnsafeLoggingDemo {

    public void login(String username, String password) {
        System.out.println("Login attempt for " + username + " with password " + password);
    }
}
```

Search:

```text
System.out.println
password
token
secret
```

Fix:

```java
package com.example.springbootpractice.securityreview;

public class UnsafeLoggingDemo {

    public void login(String username, String password) {
        System.out.println("Login attempt for user: " + username);
    }
}
```

## Practice 3 — Structural Search

Use:

```text
Find Action → Search Structurally
```

Search:

```java
System.out.println($TEXT$);
```

## Practice 4 — Vulnerable Dependencies

Open:

```text
View → Tool Windows → Vulnerable Dependencies
```

Temporarily add old dependency:

```xml
<dependency>
    <groupId>commons-collections</groupId>
    <artifactId>commons-collections</artifactId>
    <version>3.2.1</version>
</dependency>
```

Reload Maven, review warning, then remove dependency.

## Practice 5 — Add Basic Validation

In `TaskService.createTask`:

```java
public Task createTask(Task task) {
    if (task.getTitle() == null || task.getTitle().isBlank()) {
        throw new IllegalArgumentException("Task title is required");
    }

    if (task.getStatus() == null || task.getStatus().isBlank()) {
        task.setStatus("OPEN");
    }

    return taskRepository.save(task);
}
```

## Practice 6 — Global Exception Handler

Create:

```text
com.example.springbootpractice.exception.GlobalExceptionHandler
```

```java
package com.example.springbootpractice.exception;

import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(IllegalArgumentException.class)
    public ResponseEntity<String> handleIllegalArgumentException(IllegalArgumentException exception) {
        return ResponseEntity.badRequest().body(exception.getMessage());
    }
}
```

## Invalid HTTP Request

```http
### Create invalid task - blank title
POST {{baseUrl}}/tasks
Content-Type: application/json

{
  "title": "",
  "status": "OPEN"
}
```

Expected:

```text
HTTP 400
Task title is required
```

## security-review-notes.md

Create:

```text
src/test/security-review-notes.md
```

```markdown
# Security Review Notes

## Checked Areas
- Hardcoded secrets
- Unsafe logging
- Input validation
- Error handling
- Vulnerable dependencies
- Private env files
- Git diff before commit

## Findings
- Avoid logging passwords/tokens.
- Avoid hardcoded secrets.
- Validate task title.
- Do not commit private HTTP Client env files.
- Remove intentionally vulnerable dependencies after testing.

## Future Improvements
- Add authentication.
- Add authorization.
- Add DTO validation annotations.
- Add structured error response.
- Add dependency scanning in CI.
```

## .gitignore

```gitignore
.env
*.env.local
http-client.private.env.json
**/http-client.private.env.json
```

## Inspect Code

```text
Analyze → Inspect Code
```

Do not automatically fix everything; understand each warning.

## Assignment

```text
1. Create securityreview package
2. Create SecretDemo with hardcoded values
3. Review IntelliJ inspections
4. Replace with environment-based version
5. Create UnsafeLoggingDemo
6. Search System.out.println/password/token/secret
7. Fix unsafe logging
8. Use Structural Search
9. Open Vulnerable Dependencies
10. Temporarily add old commons-collections dependency
11. Reload Maven and review warning
12. Remove old dependency
13. Add validation in TaskService
14. Create GlobalExceptionHandler
15. Add invalid HTTP request
16. Confirm 400 response
17. Create security-review-notes.md
18. Update .gitignore
19. Run Inspect Code
20. Review Git diff
```

When done, reply:

```text
Module 21 completed
```


---

# Module 22 — Plugin Ecosystem

## Goal
Learn how to manage IntelliJ plugins safely and productively.

You will learn what plugins are, bundled vs Marketplace plugins, install/disable/uninstall/update, required plugins, performance/security impact, recommended plugins, and what to avoid.

## What Is a Plugin?

A plugin adds functionality to IntelliJ IDEA.

Examples:

```text
Docker support
Database tools
Markdown support
YAML support
Spring support
Kubernetes support
Security scanning
AI assistance
Themes
Language support
```

## Bundled vs Marketplace Plugins

| Type | Meaning |
|---|---|
| Bundled | Comes with IntelliJ |
| Marketplace | Installed separately |

Useful plugin areas:

```text
Git
Maven
Gradle
Terminal
HTTP Client
Docker
Database Tools and SQL
Package Checker
Markdown
YAML
```

## Open Plugin Settings

```text
Settings / Preferences → Plugins
```

Shortcuts:

```text
Mac: Cmd + ,
Windows/Linux: Ctrl + Alt + S
```

Tabs:

```text
Marketplace
Installed
Updates
```

## Marketplace Practice

Search:

```text
Markdown
Docker
Database Tools and SQL
Package Checker
CSV
YAML
Snyk
```

Check:

```text
Plugin name
Vendor
Downloads
Rating
Last updated
Compatibility
Description
Permissions/behavior
```

## Installed Tab

Search:

```text
Maven
Gradle
Git
Docker
Database
Package Checker
Markdown
YAML
HTTP Client
Spring
```

Do not disable core plugins randomly.

## Enable/Disable Practice

Only use a non-critical plugin.

```text
Settings → Plugins → Installed → Disable/Enable → Restart if requested
```

Avoid disabling:

```text
Java
Maven
Gradle
Git
Spring
Database Tools
Docker
Terminal
HTTP Client
```

## Updates

Open:

```text
Settings → Plugins → Updates
```

Good habit:

```text
Update regularly, but avoid mass updates during urgent work.
```

## Required Plugins

Open:

```text
Settings → Build, Execution, Deployment → Required Plugins
```

Useful for team projects.

## Recommended Plugins/Features

| Plugin/Feature | Why |
|---|---|
| Maven | Dependencies/build |
| Gradle | Dependencies/build |
| Git | Version control |
| Docker | Containers |
| Database Tools and SQL | DB browsing/query |
| Package Checker | Vulnerable dependency review |
| Markdown | Docs |
| YAML | Docker/config |
| HTTP Client | API testing |
| Spring | Spring Boot productivity |

## Security Plugins

Explore later:

```text
Package Checker
Snyk Security
Qodana
Black Duck Code Sight
```

Rule:

```text
Do not install security plugins into company projects without approval.
```

## Plugin Security Checklist

```text
1. Trusted vendor?
2. Known company/JetBrains?
3. Actively maintained?
4. Compatible with IDE?
5. Needs project file access?
6. Sends data externally?
7. Allowed by company policy?
8. Built-in feature already exists?
9. Really needed?
10. Easy to remove?
```

## Performance

Too many plugins can cause:

```text
Slow startup
Slow indexing
High memory
Slow completion
IDE freezes
```

## Practice Files

Create `README-practice.md`:

```markdown
# IntelliJ Plugin Practice

## Useful Plugins
- Maven
- Gradle
- Git
- Docker
- Database Tools and SQL
- Package Checker
- Markdown
- YAML
- HTTP Client

## Security Rule
Install only trusted plugins and avoid unnecessary plugins in company projects.
```

Open `docker-compose.yml` and check YAML support.

Open Database and Vulnerable Dependencies windows if available.

## Assignment

```text
1. Open Settings → Plugins
2. Review Marketplace
3. Review Installed
4. Search major plugins
5. Confirm important plugins enabled
6. Open Updates
7. Review Required Plugins
8. Create README-practice.md
9. Test Markdown preview
10. Check YAML support
11. Open Database tool window
12. Open Vulnerable Dependencies
13. Review one Marketplace plugin vendor/downloads/rating
14. Disable/re-enable non-critical plugin
15. Remove test plugin
16. Write plugin safety checklist
```

When done, reply:

```text
Module 22 completed
```


---

# Module 23 — AI-Assisted Development in IntelliJ IDEA

## Goal
Use AI inside IntelliJ responsibly and safely.

You will practice AI Chat, explaining code, generating tests, refactoring suggestions, commit messages, HTTP Client help, debugging guidance, security review prompts, privacy rules, and AI restrictions.

## Important Rule

AI is an assistant, not the final authority.

Use AI for:

```text
Explaining code
Draft tests
Small refactoring suggestions
Commit messages
Documentation drafts
Change summaries
Possible issue spotting
```

Do not blindly trust AI for:

```text
Security fixes
Authentication
Authorization
Cryptography
Production config
Dependency upgrade decisions
Database migrations
Compliance-sensitive work
```

## Check Availability

```text
Settings → Plugins → AI Assistant
View → Tool Windows → AI Assistant
Shift Shift → AI Assistant
```

## Practice 1 — Explain Code

Open `TaskController.java`, select:

```java
@GetMapping("/{id}")
public ResponseEntity<Task> getTaskById(@PathVariable Long id) {
    return taskService.getTaskById(id)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
}
```

Ask:

```text
Explain this Spring Boot controller method in simple terms.
```

Expected explanation should mention:

```text
@GetMapping
@PathVariable
Optional
ResponseEntity.ok
404
```

## Better Prompting

Bad:

```text
Explain this.
```

Better:

```text
Explain this Spring Boot controller method as if I am learning IntelliJ and Spring Boot. Focus on how request flow moves from controller to service.
```

Best:

```text
Explain this method in 5 bullet points. Then tell me where I should place a breakpoint to debug it in IntelliJ.
```

## Generate Unit Tests

Open `TaskService.java` and ask:

```text
Generate unit tests for TaskService createTask and updateTask. Use JUnit 5 and Mockito. Keep tests simple and readable.
```

Review:

```text
Imports
Framework
Mocks
Assertions
No fake methods/classes
No unnecessary complexity
```

## Review AI Diff

```text
1. Read generated code
2. Check changed files
3. Accept only useful changes
4. Reject incorrect changes
5. Run tests
6. Review Git diff
```

## Refactoring Prompt

```text
Review this service class and suggest small refactoring improvements. Do not change behavior.
```

Then:

```text
Show only the smallest safe refactoring for createTask.
```

## Commit Message Prompt

```text
Generate a concise commit message for the selected changes. Use imperative style.
```

Good:

```text
Add task validation error handling
```

Bad:

```text
Updated files
```

## HTTP Client Prompt

```text
Add HTTP Client requests to test invalid task creation and confirm blank title returns 400.
```

Expected:

```http
### Create invalid task - blank title
# @name createInvalidTaskBlankTitle
POST {{baseUrl}}/tasks
Content-Type: application/json

{
  "title": "",
  "status": "OPEN"
}

> {%
    client.test("Blank title returns 400", function () {
        client.assert(response.status === 400, "Expected status 400");
    });
%}
```

## Debugging Prompt

```text
I am debugging POST /tasks in IntelliJ. Tell me where to place breakpoints and what variables to inspect.
```

Good locations:

```text
TaskController.createTask
TaskService.createTask
TaskRepository.save
GlobalExceptionHandler
```

## Security Review Prompt

```text
Review these files for basic application security concerns. Focus on validation, error handling, logging, and access control gaps. Do not rewrite the code yet.
```

Expected gaps:

```text
No authentication
No authorization
Limited validation
Simple errors
Need DTOs
Need centralized validation
```

## Data Privacy

Do not paste/share:

```text
production passwords
API keys
customer data
private certs
tokens
company confidential code
security incident details
real customer vulnerabilities
```

## AI Review Checklist

```text
1. Code compiles?
2. Imports correct?
3. Method/class names real?
4. Behavior changed unexpectedly?
5. Too complex?
6. Sensitive data exposed?
7. Security weakened?
8. Vulnerable dependency added?
9. Tests passed?
10. Git diff reviewed?
```

## Assignment

```text
1. Confirm AI Assistant availability
2. Explain getTaskById
3. Ask breakpoint locations
4. Ask TaskService refactoring suggestions
5. Generate tests if available
6. Review AI Diff
7. Run tests
8. Generate invalid HTTP request
9. Run invalid request
10. Ask AI for security concerns
11. Generate/compare commit message
12. Review Git diff manually
13. Open AI settings
14. Review privacy options
15. Write 5 safe AI rules in README-practice.md
```

When done, reply:

```text
Module 23 completed
```


---

# Module 24 — Real-World Java/Spring Project Structure in IntelliJ IDEA

## Goal
Organize the Spring Boot project like a professional codebase and use IntelliJ refactoring safely.

You will practice controller/service/repository/model/dto/mapper/config/exception packages, request/response DTOs, mapper, entity vs API separation, Move/Rename refactoring, Find Usages, package views, and Git diff review.

## Target Structure

```text
com.example.springbootpractice
 ├── SpringbootPracticeApplication.java
 ├── config
 ├── controller
 ├── dto
 │   ├── request
 │   └── response
 ├── exception
 ├── mapper
 ├── model
 ├── repository
 ├── service
 └── securityreview
```

## Package Purpose

| Package | Purpose |
|---|---|
| controller | REST endpoints |
| service | Business logic |
| repository | Database access |
| model | JPA entities |
| dto.request | Incoming requests |
| dto.response | Outgoing responses |
| mapper | Convert entity ↔ DTO |
| exception | Error handling |
| config | Startup/config |

## TaskRequest.java

```java
package com.example.springbootpractice.dto.request;

public class TaskRequest {

    private String title;
    private String status;

    public TaskRequest() {
    }

    public TaskRequest(String title, String status) {
        this.title = title;
        this.status = status;
    }

    public String getTitle() { return title; }
    public String getStatus() { return status; }
    public void setTitle(String title) { this.title = title; }
    public void setStatus(String status) { this.status = status; }
}
```

## TaskResponse.java

```java
package com.example.springbootpractice.dto.response;

public class TaskResponse {

    private Long id;
    private String title;
    private String status;

    public TaskResponse(Long id, String title, String status) {
        this.id = id;
        this.title = title;
        this.status = status;
    }

    public Long getId() { return id; }
    public String getTitle() { return title; }
    public String getStatus() { return status; }
}
```

## TaskMapper.java

```java
package com.example.springbootpractice.mapper;

import com.example.springbootpractice.dto.request.TaskRequest;
import com.example.springbootpractice.dto.response.TaskResponse;
import com.example.springbootpractice.model.Task;
import org.springframework.stereotype.Component;

@Component
public class TaskMapper {

    public Task toEntity(TaskRequest request) {
        Task task = new Task();
        task.setTitle(request.getTitle());
        task.setStatus(request.getStatus());
        return task;
    }

    public TaskResponse toResponse(Task task) {
        return new TaskResponse(task.getId(), task.getTitle(), task.getStatus());
    }
}
```

## Update TaskController.java

```java
package com.example.springbootpractice.controller;

import com.example.springbootpractice.dto.request.TaskRequest;
import com.example.springbootpractice.dto.response.TaskResponse;
import com.example.springbootpractice.mapper.TaskMapper;
import com.example.springbootpractice.model.Task;
import com.example.springbootpractice.service.TaskService;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/tasks")
public class TaskController {

    private final TaskService taskService;
    private final TaskMapper taskMapper;

    public TaskController(TaskService taskService, TaskMapper taskMapper) {
        this.taskService = taskService;
        this.taskMapper = taskMapper;
    }

    @GetMapping
    public List<TaskResponse> getAllTasks() {
        return taskService.getAllTasks().stream().map(taskMapper::toResponse).toList();
    }

    @GetMapping("/{id}")
    public ResponseEntity<TaskResponse> getTaskById(@PathVariable Long id) {
        return taskService.getTaskById(id)
                .map(taskMapper::toResponse)
                .map(ResponseEntity::ok)
                .orElse(ResponseEntity.notFound().build());
    }

    @PostMapping
    public ResponseEntity<TaskResponse> createTask(@RequestBody TaskRequest request) {
        Task task = taskMapper.toEntity(request);
        Task createdTask = taskService.createTask(task);
        return ResponseEntity.ok(taskMapper.toResponse(createdTask));
    }

    @PutMapping("/{id}")
    public ResponseEntity<TaskResponse> updateTask(@PathVariable Long id, @RequestBody TaskRequest request) {
        Task task = taskMapper.toEntity(request);
        return taskService.updateTask(id, task)
                .map(taskMapper::toResponse)
                .map(ResponseEntity::ok)
                .orElse(ResponseEntity.notFound().build());
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteTask(@PathVariable Long id) {
        boolean deleted = taskService.deleteTask(id);
        return deleted ? ResponseEntity.noContent().build() : ResponseEntity.notFound().build();
    }
}
```

## Test

```http
GET {{baseUrl}}/tasks
```

```http
POST {{baseUrl}}/tasks
Content-Type: application/json

{
  "title": "Practice DTO structure",
  "status": "OPEN"
}
```

## Refactoring Practice

Find Usages on:

```text
Task
TaskRequest
TaskResponse
TaskMapper
toResponse
toEntity
```

Move `TaskController` temporarily to package `web` using `F6`, test app, then move it back.

Rename `dto.response` to `dto.out` using `Shift + F6`, check imports, then rename back.

## Git Diff

Review:

```text
Added TaskRequest
Added TaskResponse
Added TaskMapper
Updated TaskController
```

Commit:

```text
Refactor task API to use DTO structure
```

## Assignment

```text
1. Create dto.request
2. Create dto.response
3. Create mapper
4. Create TaskRequest
5. Create TaskResponse
6. Create TaskMapper
7. Update TaskController
8. Reformat code
9. Test GET /tasks
10. Test POST /tasks
11. Find Usages on TaskMapper and TaskRequest
12. Move TaskController to web and back
13. Rename dto.response to dto.out and back
14. Review package view
15. Review Git diff
16. Commit refactor
```

When done, reply:

```text
Module 24 completed
```


---

# Module 25 — Working with Large Codebases in IntelliJ IDEA

## Goal
Learn how to survive and understand large enterprise codebases.

You will practice indexing awareness, entry point discovery, annotation/path searches, request flow tracing, stack trace analysis, multi-module awareness, build tool windows, dependency navigation, excluding heavy folders, and performance habits.

## Mindset

Do not try to understand everything.

First find:

```text
Entry point
Main packages
Request flow
Build system
How to run app
How to test/debug one feature
```

## First 10-Minute Checklist

```text
1. Maven, Gradle, or multi-module?
2. Where is pom.xml/build.gradle?
3. Root package?
4. Main Spring Boot class?
5. Controllers?
6. Services?
7. Repositories?
8. Config files?
9. How to run?
10. How to test one endpoint?
```

For your project:

```text
Build file       → pom.xml
Main class       → SpringbootPracticeApplication
Controllers      → controller
Services         → service
Repositories     → repository
Config           → application.properties, config
HTTP tests       → src/test/http
Docker           → docker-compose.yml
```

## Indexing

Indexing means IntelliJ reads project files and builds search/navigation data. Let indexing finish before judging performance.

## Find Entry Point

Use:

```text
Shift Shift → Application
```

Open `SpringbootPracticeApplication`.

## Identify Request Flow

```text
HTTP request
→ TaskController
→ TaskService
→ TaskRepository
→ Database
```

Open in order using Search Everywhere:

```text
TaskController
TaskService
TaskRepository
Task
TaskRequest
TaskResponse
TaskMapper
```

## Search by Annotation

Find in Files:

```text
@RestController
@Service
@Repository
@Configuration
@RequestMapping
@GetMapping
@PostMapping
@PutMapping
@DeleteMapping
```

## Search by API Path

Search:

```text
/tasks
```

Also search domain words:

```text
task
order
user
auth
payment
customer
```

## File Structure

Open `TaskController`:

```text
Cmd + F12 / Ctrl + F12
```

Jump to methods.

## Find Usages Before Changing

Use:

```text
Option + F7 / Alt + F7
```

Practice on:

```text
TaskService.createTask
TaskMapper.toResponse
TaskRepository
TaskRequest
TaskResponse
```

## Declaration/Implementation

| Action | Mac | Windows/Linux |
|---|---|---|
| Declaration | `Cmd + Click` | `Ctrl + Click` |
| Implementation | `Cmd + Option + B` | `Ctrl + Alt + B` |
| Back | `Cmd + Option + Left` | `Ctrl + Alt + Left` |

## Stack Traces

Rule:

```text
Find first line from your package: com.example.springbootpractice
```

Use:

```text
Analyze → Stack Trace or Thread Dump
```

Paste stack trace from logs/CI/Slack/Jira.

## Multi-Module Awareness

Maven example:

```text
company-platform
 ├── pom.xml
 ├── api/pom.xml
 ├── service/pom.xml
 ├── repository/pom.xml
 ├── common/pom.xml
 └── integration-tests/pom.xml
```

Always know which module contains your change.

## Maven/Gradle Tool Windows

Use to reload project, run module-specific goals, inspect dependencies, find build failures, and run focused tests.

## Exclude Heavy Folders

Possible folders:

```text
target
build
node_modules
logs
large reports
coverage output
temporary data
```

Use:

```text
Right-click folder → Mark Directory as → Excluded
```

Do not exclude source folders.

## Performance Habits

```text
1. Let indexing finish
2. Disable unused plugins
3. Exclude non-source heavy folders
4. Unload modules not needed
5. Increase memory if needed
6. Avoid huge generated files
7. Restart after plugin/config changes
```

## Investigation Scenario

Issue:

```text
POST /tasks with blank title should return 400.
```

Steps:

```text
1. Search /tasks
2. Open TaskController
3. Jump to createTask
4. Go to TaskService.createTask
5. Find validation
6. Open GlobalExceptionHandler
7. Run invalid POST
8. Debug if needed
9. Review response
```

## Notes File

Create:

```text
src/test/large-codebase-notes.md
```

```markdown
# Large Codebase Investigation Notes

## Entry Point
- Main class:

## Build System
- Maven or Gradle:

## Main Packages
- controller:
- service:
- repository:
- model:
- dto:
- config:
- exception:

## How to Run
- Run configuration:

## How to Test
- HTTP file:
- Key endpoint:

## Debug Flow
- Controller:
- Service:
- Repository:

## Common Checks
- Search by endpoint path
- Search by annotation
- Find usages before editing
- Read first stack trace line from our package
- Review Git diff before commit
```

## Assignment

```text
1. Open springboot-practice
2. Wait for indexing
3. Find main app class
4. Find TaskController
5. Search annotations
6. Search /tasks
7. Use File Structure
8. Find Usages on TaskMapper.toResponse
9. Go Controller → Service → Repository
10. Run invalid POST
11. Debug Controller → Service
12. Open Maven tool window
13. Identify build/config files
14. Review excluded folders
15. Open Analyze Stack Trace
16. Create large-codebase-notes.md
17. Fill notes
18. Review Git diff
```

When done, reply:

```text
Module 25 completed
```


---

# Module 26 — Capstone: Secure Task Manager API

## Goal
Combine everything into the final Secure Task Manager API.

This capstone uses project structure, Spring Boot run configuration, Maven dependencies, REST API, DTOs, validation, exception handling, database integration, Docker PostgreSQL, HTTP Client testing, debugging, Git review workflow, security review, and README documentation.

## Final Structure

```text
springboot-practice
 ├── docker-compose.yml
 ├── pom.xml
 ├── README.md
 ├── src/main/java/com.example.springbootpractice
 │   ├── SpringbootPracticeApplication.java
 │   ├── config/DataInitializer.java
 │   ├── controller/TaskController.java
 │   ├── dto/request/TaskRequest.java
 │   ├── dto/response/ApiErrorResponse.java
 │   ├── dto/response/TaskResponse.java
 │   ├── exception/GlobalExceptionHandler.java
 │   ├── mapper/TaskMapper.java
 │   ├── model/Task.java
 │   ├── repository/TaskRepository.java
 │   └── service/TaskService.java
 └── src/test
     ├── http/http-client.env.json
     ├── http/task-api-capstone.http
     └── security-review-notes.md
```

## pom.xml Dependencies

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-validation</artifactId>
    </dependency>

    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <scope>runtime</scope>
    </dependency>

    <dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
        <scope>runtime</scope>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

## Task.java

```java
package com.example.springbootpractice.model;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;

@Entity
public class Task {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;
    private String status;

    public Task() {
    }

    public Task(String title, String status) {
        this.title = title;
        this.status = status;
    }

    public Task(Long id, String title, String status) {
        this.id = id;
        this.title = title;
        this.status = status;
    }

    public Long getId() { return id; }
    public String getTitle() { return title; }
    public String getStatus() { return status; }
    public void setId(Long id) { this.id = id; }
    public void setTitle(String title) { this.title = title; }
    public void setStatus(String status) { this.status = status; }
}
```

## TaskRequest.java

```java
package com.example.springbootpractice.dto.request;

import jakarta.validation.constraints.NotBlank;
import jakarta.validation.constraints.Pattern;
import jakarta.validation.constraints.Size;

public class TaskRequest {

    @NotBlank(message = "Task title is required")
    @Size(max = 100, message = "Task title must not exceed 100 characters")
    private String title;

    @Pattern(
            regexp = "OPEN|IN_PROGRESS|COMPLETED",
            message = "Status must be OPEN, IN_PROGRESS, or COMPLETED"
    )
    private String status;

    public TaskRequest() {
    }

    public TaskRequest(String title, String status) {
        this.title = title;
        this.status = status;
    }

    public String getTitle() { return title; }
    public String getStatus() { return status; }
    public void setTitle(String title) { this.title = title; }
    public void setStatus(String status) { this.status = status; }
}
```

## TaskResponse.java

```java
package com.example.springbootpractice.dto.response;

public class TaskResponse {

    private Long id;
    private String title;
    private String status;

    public TaskResponse(Long id, String title, String status) {
        this.id = id;
        this.title = title;
        this.status = status;
    }

    public Long getId() { return id; }
    public String getTitle() { return title; }
    public String getStatus() { return status; }
}
```

## ApiErrorResponse.java

```java
package com.example.springbootpractice.dto.response;

import java.time.LocalDateTime;
import java.util.List;

public class ApiErrorResponse {

    private LocalDateTime timestamp;
    private int status;
    private String error;
    private List<String> messages;

    public ApiErrorResponse(int status, String error, List<String> messages) {
        this.timestamp = LocalDateTime.now();
        this.status = status;
        this.error = error;
        this.messages = messages;
    }

    public LocalDateTime getTimestamp() { return timestamp; }
    public int getStatus() { return status; }
    public String getError() { return error; }
    public List<String> getMessages() { return messages; }
}
```

## TaskMapper.java

```java
package com.example.springbootpractice.mapper;

import com.example.springbootpractice.dto.request.TaskRequest;
import com.example.springbootpractice.dto.response.TaskResponse;
import com.example.springbootpractice.model.Task;
import org.springframework.stereotype.Component;

@Component
public class TaskMapper {

    public Task toEntity(TaskRequest request) {
        Task task = new Task();
        task.setTitle(request.getTitle());
        task.setStatus(request.getStatus());
        return task;
    }

    public TaskResponse toResponse(Task task) {
        return new TaskResponse(task.getId(), task.getTitle(), task.getStatus());
    }
}
```

## TaskRepository.java

```java
package com.example.springbootpractice.repository;

import com.example.springbootpractice.model.Task;
import org.springframework.data.jpa.repository.JpaRepository;

public interface TaskRepository extends JpaRepository<Task, Long> {
}
```

## TaskService.java

```java
package com.example.springbootpractice.service;

import com.example.springbootpractice.model.Task;
import com.example.springbootpractice.repository.TaskRepository;
import org.springframework.stereotype.Service;

import java.util.List;
import java.util.Optional;

@Service
public class TaskService {

    private static final String DEFAULT_STATUS = "OPEN";
    private final TaskRepository taskRepository;

    public TaskService(TaskRepository taskRepository) {
        this.taskRepository = taskRepository;
    }

    public List<Task> getAllTasks() {
        return taskRepository.findAll();
    }

    public Optional<Task> getTaskById(Long id) {
        return taskRepository.findById(id);
    }

    public Task createTask(Task task) {
        applyDefaultStatusIfMissing(task);
        return taskRepository.save(task);
    }

    public Optional<Task> updateTask(Long id, Task updatedTask) {
        return taskRepository.findById(id).map(existingTask -> {
            existingTask.setTitle(updatedTask.getTitle());
            existingTask.setStatus(resolveStatus(updatedTask.getStatus()));
            return taskRepository.save(existingTask);
        });
    }

    public boolean deleteTask(Long id) {
        if (!taskRepository.existsById(id)) {
            return false;
        }
        taskRepository.deleteById(id);
        return true;
    }

    private void applyDefaultStatusIfMissing(Task task) {
        task.setStatus(resolveStatus(task.getStatus()));
    }

    private String resolveStatus(String status) {
        if (status == null || status.isBlank()) {
            return DEFAULT_STATUS;
        }
        return status;
    }
}
```

## TaskController.java

```java
package com.example.springbootpractice.controller;

import com.example.springbootpractice.dto.request.TaskRequest;
import com.example.springbootpractice.dto.response.TaskResponse;
import com.example.springbootpractice.mapper.TaskMapper;
import com.example.springbootpractice.model.Task;
import com.example.springbootpractice.service.TaskService;
import jakarta.validation.Valid;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/tasks")
public class TaskController {

    private final TaskService taskService;
    private final TaskMapper taskMapper;

    public TaskController(TaskService taskService, TaskMapper taskMapper) {
        this.taskService = taskService;
        this.taskMapper = taskMapper;
    }

    @GetMapping
    public List<TaskResponse> getAllTasks() {
        return taskService.getAllTasks().stream().map(taskMapper::toResponse).toList();
    }

    @GetMapping("/{id}")
    public ResponseEntity<TaskResponse> getTaskById(@PathVariable Long id) {
        return taskService.getTaskById(id)
                .map(taskMapper::toResponse)
                .map(ResponseEntity::ok)
                .orElse(ResponseEntity.notFound().build());
    }

    @PostMapping
    public ResponseEntity<TaskResponse> createTask(@Valid @RequestBody TaskRequest request) {
        Task task = taskMapper.toEntity(request);
        Task createdTask = taskService.createTask(task);
        return ResponseEntity.ok(taskMapper.toResponse(createdTask));
    }

    @PutMapping("/{id}")
    public ResponseEntity<TaskResponse> updateTask(@PathVariable Long id, @Valid @RequestBody TaskRequest request) {
        Task task = taskMapper.toEntity(request);
        return taskService.updateTask(id, task)
                .map(taskMapper::toResponse)
                .map(ResponseEntity::ok)
                .orElse(ResponseEntity.notFound().build());
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteTask(@PathVariable Long id) {
        boolean deleted = taskService.deleteTask(id);
        return deleted ? ResponseEntity.noContent().build() : ResponseEntity.notFound().build();
    }
}
```

## GlobalExceptionHandler.java

```java
package com.example.springbootpractice.exception;

import com.example.springbootpractice.dto.response.ApiErrorResponse;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

import java.util.List;

@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ApiErrorResponse> handleValidationException(MethodArgumentNotValidException exception) {
        List<String> messages = exception.getBindingResult()
                .getFieldErrors()
                .stream()
                .map(error -> error.getField() + ": " + error.getDefaultMessage())
                .toList();

        ApiErrorResponse response = new ApiErrorResponse(400, "Validation Failed", messages);
        return ResponseEntity.badRequest().body(response);
    }

    @ExceptionHandler(IllegalArgumentException.class)
    public ResponseEntity<ApiErrorResponse> handleIllegalArgumentException(IllegalArgumentException exception) {
        ApiErrorResponse response = new ApiErrorResponse(400, "Bad Request", List.of(exception.getMessage()));
        return ResponseEntity.badRequest().body(response);
    }
}
```

## DataInitializer.java

```java
package com.example.springbootpractice.config;

import com.example.springbootpractice.model.Task;
import com.example.springbootpractice.repository.TaskRepository;
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

@Component
public class DataInitializer implements CommandLineRunner {

    private final TaskRepository taskRepository;

    public DataInitializer(TaskRepository taskRepository) {
        this.taskRepository = taskRepository;
    }

    @Override
    public void run(String... args) {
        if (taskRepository.count() == 0) {
            taskRepository.save(new Task("Complete IntelliJ IDEA capstone", "OPEN"));
            taskRepository.save(new Task("Review API security checklist", "IN_PROGRESS"));
        }
    }
}
```

## application.properties

```properties
spring.application.name=springboot-practice

spring.datasource.url=jdbc:postgresql://localhost:5432/taskdb
spring.datasource.username=taskuser
spring.datasource.password=taskpass
spring.datasource.driver-class-name=org.postgresql.Driver

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

server.port=8080
```

## task-api-capstone.http

```http
### Get all tasks
# @name getAllTasks
GET {{baseUrl}}/tasks

### Get task by ID
# @name getTaskById
GET {{baseUrl}}/tasks/{{taskId}}

### Create valid task
# @name createValidTask
POST {{baseUrl}}/tasks
Content-Type: application/json

{
  "title": "Created from capstone HTTP Client",
  "status": "OPEN"
}

### Create task without status - should default to OPEN
# @name createTaskWithoutStatus
POST {{baseUrl}}/tasks
Content-Type: application/json

{
  "title": "Task without status"
}

### Create invalid task - blank title
# @name createInvalidTaskBlankTitle
POST {{baseUrl}}/tasks
Content-Type: application/json

{
  "title": "",
  "status": "OPEN"
}

> {%
    client.test("Blank title returns 400", function () {
        client.assert(response.status === 400, "Expected status 400");
    });
%}

### Create invalid task - invalid status
# @name createInvalidTaskStatus
POST {{baseUrl}}/tasks
Content-Type: application/json

{
  "title": "Invalid status test",
  "status": "DONE"
}

> {%
    client.test("Invalid status returns 400", function () {
        client.assert(response.status === 400, "Expected status 400");
    });
%}

### Update task
# @name updateTask
PUT {{baseUrl}}/tasks/{{taskId}}
Content-Type: application/json

{
  "title": "Updated from capstone HTTP Client",
  "status": "COMPLETED"
}

### Delete task
# @name deleteTask
DELETE {{baseUrl}}/tasks/{{taskId}}
```

## http-client.env.json

```json
{
  "local": {
    "baseUrl": "http://localhost:8080",
    "taskId": "1"
  },
  "local8081": {
    "baseUrl": "http://localhost:8081",
    "taskId": "1"
  }
}
```

## .gitignore

```gitignore
target/
.env
*.env.local
http-client.private.env.json
**/http-client.private.env.json
```

## Capstone Workflow

```text
1. Start Docker PostgreSQL from Services
2. Run Spring Boot app from Services
3. Open task-api-capstone.http
4. Run GET /tasks
5. Run POST valid task
6. Run POST invalid blank title
7. Confirm 400 validation response
8. Run PUT task
9. Run DELETE task
10. Debug POST /tasks
11. Step from TaskController to TaskService
12. Inspect task request values
13. Open Database tool window
14. Run SELECT * FROM task;
15. Review Git diff
16. Commit final capstone changes
```

## security-review-notes.md

```markdown
# Security Review Notes

## Implemented
- Request DTO added.
- Response DTO added.
- Entity is no longer directly used as request body.
- Task title validation added.
- Task status validation added.
- Global exception handler added.
- Error response format added.
- Private HTTP Client environment file ignored by Git.
- Basic API testing added through IntelliJ HTTP Client.

## Current Gaps
- Authentication is not implemented.
- Authorization is not implemented.
- DELETE and PUT endpoints are not protected.
- Audit logging is not implemented.
- Rate limiting is not implemented.
- Production secret management is not implemented.

## Future Improvements
- Add Spring Security.
- Add role-based access control.
- Use environment variables or secret manager for real credentials.
- Add structured logging.
- Add integration tests.
- Add CI pipeline checks.
- Add dependency vulnerability scanning.
```

## README.md

```markdown
# Secure Task Manager API

This is the final IntelliJ IDEA learning capstone project.

## Technology Stack
- Java 21
- Spring Boot
- Maven
- Spring Web
- Spring Data JPA
- PostgreSQL with Docker Compose
- IntelliJ HTTP Client

## Main Features
- Create task
- Get all tasks
- Get task by ID
- Update task
- Delete task
- Request validation
- Global error handling
- DTO-based API structure
- Database persistence with PostgreSQL

## How to Run

### 1. Start PostgreSQL

```bash
docker compose up -d
```

### 2. Run Spring Boot App

Run this class from IntelliJ:

```text
SpringbootPracticeApplication
```

### 3. Test API

Open:

```text
src/test/http/task-api-capstone.http
```

Run requests from IntelliJ HTTP Client.

## API Endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| GET | /tasks | Get all tasks |
| GET | /tasks/{id} | Get task by ID |
| POST | /tasks | Create task |
| PUT | /tasks/{id} | Update task |
| DELETE | /tasks/{id} | Delete task |

## Security Notes
- Request validation is implemented.
- Global validation error response is implemented.
- DTOs are used to avoid exposing entity directly.
- Authentication and authorization are future improvements.
```

## Final Commit

Do not commit:

```text
http-client.private.env.json
.env
target/
temporary debug files
old vulnerable dependency practice
```

Commit:

```text
Complete secure task manager API capstone
```

## Assignment

```text
1. Add validation dependency
2. Reload Maven
3. Update TaskRequest
4. Add ApiErrorResponse
5. Update GlobalExceptionHandler
6. Confirm Task entity
7. Confirm TaskResponse output
8. Confirm TaskMapper
9. Confirm @Valid
10. Confirm default OPEN status
11. Start PostgreSQL Docker
12. Run Spring Boot
13. Run GET /tasks
14. Run valid POST
15. Run invalid blank-title POST
16. Confirm 400
17. Run invalid status POST
18. Confirm 400
19. Debug POST /tasks
20. Step into TaskService
21. Check database table
22. Update security-review-notes.md
23. Update README.md
24. Review Git diff
25. Commit final capstone
```

When done, reply:

```text
Capstone completed
```
