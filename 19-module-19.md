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
