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
