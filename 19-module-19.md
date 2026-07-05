# Module 19 — Advanced Debugging in IntelliJ IDEA Community Edition

## Goal

In this module, you will learn advanced debugging in **IntelliJ IDEA Community Edition**.

This module follows the same debugging goal as the original course module:

```text
HTTP request
→ Controller
→ Service
→ Repository
→ Database
```

Community Edition difference:

```text
We will not use Ultimate-only Spring Boot Services/dashboard features.
We will use normal Run/Debug, Terminal, curl, breakpoints, and the Java debugger.
```

Important:

```text
Do not change your project structure for this module.
Use the same TaskController, TaskService, TaskRepository, DTOs, mapper, or model classes that already exist in your project.
```

If your project has:

```java
TaskResponse
TaskMapper
TaskRequest
```

use them.

If your project has the simpler:

```java
Task
```

use that.

The debugging technique is the same.

---

## 1. What You Will Learn

You will learn how to use:

```text
Breakpoints
Step Into
Step Over
Step Out
Resume
Evaluate Expression
Watches
Conditional breakpoints
Logpoints
Exception breakpoints
Call stack / Frames
Debugging GET requests
Debugging POST requests
Debugging validation errors
Debugging database save flow
```

---

## 2. Community Edition Debugging Rule

In IntelliJ IDEA Community Edition, run Spring Boot as a normal Java application.

You should start debugging from:

```text
SpringbootPracticeApplication.java
```

or whatever your main application class is called.

Example:

```java
@SpringBootApplication
public class SpringbootPracticeApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootPracticeApplication.class, args);
    }
}
```

In Community Edition:

```text
Open main class
Click the bug icon
Run app in Debug mode
Send request using curl/browser/Postman
Debugger stops at your breakpoint
```

---

## 3. Important Debugging Shortcuts

| Action | Mac | Windows/Linux |
|---|---|---|
| Start Debug | `Ctrl + D` | `Shift + F9` |
| Toggle Breakpoint | `Cmd + F8` | `Ctrl + F8` |
| View Breakpoints | `Cmd + Shift + F8` | `Ctrl + Shift + F8` |
| Step Over | `F8` | `F8` |
| Step Into | `F7` | `F7` |
| Step Out | `Shift + F8` | `Shift + F8` |
| Resume Program | `Cmd + Option + R` | `F9` |
| Evaluate Expression | `Option + F8` | `Alt + F8` |
| Run to Cursor | `Option + F9` | `Alt + F9` |
| Show Execution Point | `Option + F10` | `Alt + F10` |
| Stop Debugging | `Cmd + F2` | `Ctrl + F2` |

If a shortcut does not work, use:

| Action | Mac | Windows/Linux |
|---|---|---|
| Find Action | `Cmd + Shift + A` | `Ctrl + Shift + A` |

Then search the action name.

Example:

```text
Evaluate Expression
View Breakpoints
Run to Cursor
Show Execution Point
```

---

## 4. Start the Application in Debug Mode

Open:

```text
SpringbootPracticeApplication.java
```

Click the **bug icon** near the `main()` method.

Or use:

| Mac | Windows/Linux |
|---|---|
| `Ctrl + D` | `Shift + F9` |

Expected console log:

```text
Tomcat started on port 8080
Started SpringbootPracticeApplication
```

Now the app is running in Debug mode.

---

## 5. How to Find the Controller Method

Open your controller file.

Usually it is:

```text
TaskController.java
```

Use:

```text
Shift Shift
```

Search:

```text
TaskController
```

Open the file.

Now use **File Structure** to find methods.

| Mac | Windows/Linux |
|---|---|
| `Cmd + F12` | `Ctrl + F12` |

Look for methods like:

```text
getAllTasks
getTaskById
createTask
updateTask
deleteTask
```

If you cannot find the method, use **Find in Files**:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Shift + F` | `Ctrl + Shift + F` |

Search for:

```text
@GetMapping
```

```text
@PostMapping
```

```text
/tasks
```

```text
createTask
```

```text
getAllTasks
```

---

## 6. Debug GET `/tasks`

Find the method that handles:

```text
GET /tasks
```

It may look like this if your project uses DTOs:

```java
@GetMapping
public List<TaskResponse> getAllTasks() {
    return taskService.getAllTasks()
            .stream()
            .map(taskMapper::toResponse)
            .toList();
}
```

Or it may look like this if your project uses the entity directly:

```java
@GetMapping
public List<Task> getAllTasks() {
    return taskService.getAllTasks();
}
```

Both are fine.

Set a breakpoint inside this method.

Good breakpoint location:

```java
return taskService.getAllTasks()
```

or:

```java
return taskService.getAllTasks();
```

Now open IntelliJ Terminal:

| Mac | Windows/Linux |
|---|---|
| `Option + F12` | `Alt + F12` |

Run:

```bash
curl http://localhost:8080/tasks
```

Expected behavior:

```text
Debugger stops at the breakpoint.
curl waits until you resume the program.
```

---

## 7. Inspect Variables

When the debugger stops, look at the Debug window.

Important areas:

```text
Frames
Variables
Watches
Console
Threads
```

In the controller, inspect:

```text
this
taskService
taskMapper, if your project has it
request variables, if available
```

If the method is simple, there may not be many variables. That is normal.

---

## 8. Step Into the Service Layer

When stopped at:

```java
taskService.getAllTasks()
```

press:

```text
F7
```

This is **Step Into**.

You should move from:

```text
TaskController
```

to:

```text
TaskService
```

You may see a method like:

```java
public List<Task> getAllTasks() {
    return taskRepository.findAll();
}
```

or your equivalent service method.

This confirms the request flow:

```text
Controller → Service
```

---

## 9. Step Over Repository Calls

Inside the service, you may see:

```java
return taskRepository.findAll();
```

Use:

```text
F8
```

This is **Step Over**.

Reason:

```text
Repository methods are Spring Data JPA framework calls.
Usually you do not need to step into framework internals.
```

Rule:

```text
Step Into your own code.
Step Over framework/library code.
```

---

## 10. Resume the Program

After inspecting values, continue the request.

Use:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Option + R` | `F9` |

The curl request should now complete and return JSON.

---

## 11. Debug GET `/tasks/{id}`

Find the controller method for:

```text
GET /tasks/{id}
```

It may look similar to:

```java
@GetMapping("/{id}")
public ResponseEntity<TaskResponse> getTaskById(@PathVariable Long id) {
    return taskService.getTaskById(id)
            .map(taskMapper::toResponse)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
}
```

or:

```java
@GetMapping("/{id}")
public ResponseEntity<Task> getTaskById(@PathVariable Long id) {
    return taskService.getTaskById(id)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
}
```

Set a breakpoint on the line that calls:

```java
taskService.getTaskById(id)
```

Run:

```bash
curl -i http://localhost:8080/tasks/1
```

Inspect:

```text
id
taskService
Optional result after service call
```

Then test a missing record:

```bash
curl -i http://localhost:8080/tasks/999
```

Expected:

```text
HTTP/1.1 404
```

Debugging this teaches how missing database records become `404 Not Found`.

---

## 12. Debug POST `/tasks`

Find the controller method for:

```text
POST /tasks
```

It may look like this if your project uses DTOs:

```java
@PostMapping
public ResponseEntity<TaskResponse> createTask(@Valid @RequestBody TaskRequest request) {
    Task task = taskMapper.toEntity(request);
    Task createdTask = taskService.createTask(task);
    return ResponseEntity.ok(taskMapper.toResponse(createdTask));
}
```

Or it may look like this if your project uses the entity directly:

```java
@PostMapping
public ResponseEntity<Task> createTask(@RequestBody Task task) {
    return ResponseEntity.ok(taskService.createTask(task));
}
```

Use the version that exists in your project.

Set breakpoints on important lines.

For DTO version:

```java
Task task = taskMapper.toEntity(request);
Task createdTask = taskService.createTask(task);
return ResponseEntity.ok(taskMapper.toResponse(createdTask));
```

For simple entity version:

```java
return ResponseEntity.ok(taskService.createTask(task));
```

Now send a POST request:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Advanced debugging task","status":"OPEN"}'
```

Expected:

```text
Debugger stops inside the create task controller method.
```

---

## 13. Inspect POST Request Body

If your method uses `TaskRequest`, inspect:

```text
request
request.title
request.status
```

or use Evaluate Expression:

```java
request.getTitle()
```

```java
request.getStatus()
```

If your method uses `Task`, inspect:

```text
task
task.title
task.status
```

or use:

```java
task.getTitle()
```

```java
task.getStatus()
```

Expected values:

```text
Advanced debugging task
OPEN
```

---

## 14. Step Through Mapper If Your Project Has One

If your project has:

```java
taskMapper.toEntity(request)
```

press:

```text
F7
```

to step into mapper code.

You may see something like:

```java
public Task toEntity(TaskRequest request) {
    Task task = new Task();
    task.setTitle(request.getTitle());
    task.setStatus(request.getStatus());
    return task;
}
```

Inspect:

```text
request.title
request.status
task.title
task.status
```

Then press:

```text
Shift + F8
```

to Step Out back to the controller.

If your project does not have a mapper, skip this section.

---

## 15. Step Into `TaskService.createTask()`

From the controller, step into:

```java
taskService.createTask(...)
```

Use:

```text
F7
```

You should enter the service method that creates a task.

It may look similar to:

```java
public Task createTask(Task task) {
    return taskRepository.save(task);
}
```

or your equivalent code.

Set a breakpoint inside this service method.

Good breakpoint location:

```java
return taskRepository.save(task);
```

If your service uses a local variable, it may look like:

```java
Task savedTask = taskRepository.save(task);
return savedTask;
```

In that case, set breakpoint on:

```java
return savedTask;
```

---

## 16. Debug Database Save

When you reach:

```java
taskRepository.save(task)
```

use:

```text
F8
```

Do not step deep into Spring Data JPA unless you specifically want framework internals.

After the save, inspect:

```text
saved task id
saved task title
saved task status
```

If your entity uses generated IDs, the ID may be `null` before save and populated after save.

---

## 17. Check Database After POST

If using H2 Console:

```text
http://localhost:8080/h2-console
```

Run:

```sql
SELECT * FROM TASK;
```

If using PostgreSQL Docker:

```bash
docker exec -it task-postgres psql -U taskuser -d taskdb
```

Then run:

```sql
SELECT * FROM task;
```

You should see the task created during debugging.

---

## 18. Debug PUT `/tasks/{id}`

Find the controller method for:

```text
PUT /tasks/{id}
```

It may look similar to:

```java
@PutMapping("/{id}")
public ResponseEntity<TaskResponse> updateTask(@PathVariable Long id,
                                               @Valid @RequestBody TaskRequest request) {
    Task task = taskMapper.toEntity(request);
    return taskService.updateTask(id, task)
            .map(taskMapper::toResponse)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
}
```

or:

```java
@PutMapping("/{id}")
public ResponseEntity<Task> updateTask(@PathVariable Long id, @RequestBody Task task) {
    return taskService.updateTask(id, task)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
}
```

Set breakpoint on the service call:

```java
taskService.updateTask(...)
```

Run:

```bash
curl -i -X PUT http://localhost:8080/tasks/1 \
  -H "Content-Type: application/json" \
  -d '{"title":"Updated during debugging","status":"COMPLETED"}'
```

Inspect:

```text
id
request or task
title
status
existing task
updated task
saved task
```

---

## 19. Debug DELETE `/tasks/{id}`

Find the controller method for:

```text
DELETE /tasks/{id}
```

It may look similar to:

```java
@DeleteMapping("/{id}")
public ResponseEntity<Void> deleteTask(@PathVariable Long id) {
    if (taskService.deleteTask(id)) {
        return ResponseEntity.noContent().build();
    }

    return ResponseEntity.notFound().build();
}
```

Set breakpoint on:

```java
taskService.deleteTask(id)
```

Run:

```bash
curl -i -X DELETE http://localhost:8080/tasks/1
```

Step into the service method and inspect:

```text
id
existsById result
deleteById call
return value
```

Then call the same request again:

```bash
curl -i -X DELETE http://localhost:8080/tasks/1
```

Expected second result may be:

```text
HTTP/1.1 404
```

---

## 20. Conditional Breakpoints

A conditional breakpoint stops only when a condition is true.

Example:

In your `getTaskById` controller method, set a breakpoint on:

```java
taskService.getTaskById(id)
```

Right-click the breakpoint.

Add condition:

```java
id == 999
```

Now run:

```bash
curl http://localhost:8080/tasks/1
```

Debugger should not stop.

Run:

```bash
curl http://localhost:8080/tasks/999
```

Debugger should stop.

Useful conditional breakpoint examples:

```java
id == 1
```

```java
id == 999
```

```java
task.getTitle() == null
```

```java
task.getTitle().isBlank()
```

```java
"COMPLETED".equals(task.getStatus())
```

---

## 21. Logpoints

A logpoint prints a message without stopping the app.

This is useful when:

```text
You want to observe execution
You do not want to pause the request
A method is called many times
You want temporary debug logging without changing code
```

Set a breakpoint inside your service create method, for example:

```text
TaskService.createTask()
```

Meaning:

```text
Open TaskService.java
Find the createTask method
Set breakpoint inside that method
```

Right-click the breakpoint.

Change:

```text
Uncheck Suspend
Enable Log message to console
```

Example log message:

```text
createTask method called
```

Now send:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Logpoint test","status":"OPEN"}'
```

Expected:

```text
The app does not stop.
A message appears in the debug console.
```

---

## 22. Exception Breakpoints

Exception breakpoints stop when a specific exception occurs.

Open View Breakpoints:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Shift + F8` | `Ctrl + Shift + F8` |

Click:

```text
+
```

Choose:

```text
Java Exception Breakpoint
```

Add:

```text
NullPointerException
```

Now IntelliJ can stop when a `NullPointerException` is thrown.

---

## 23. Practice Exception Debugging

Create a temporary controller only for practice if the original module includes this exercise.

Create:

```text
DebugErrorController.java
```

Example:

```java
package com.example.springbootpractice.controller;

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

Run app in Debug mode.

Call:

```bash
curl http://localhost:8080/debug/error
```

Expected:

```text
Debugger stops on the NullPointerException.
```

After practice:

```text
Delete DebugErrorController
or keep it only in a learning branch
```

Do not leave debug-only code in production-style commits.

---

## 24. Read Stack Trace Correctly

When an exception happens, look for your package first.

Example:

```text
com.example.springbootpractice.controller.DebugErrorController.error(DebugErrorController.java:10)
```

Rule:

```text
Find the first stack trace line that points to your code.
Start debugging there.
```

Do not start with framework lines like:

```text
org.springframework...
org.apache.catalina...
jakarta.servlet...
```

Those are usually not where your bug begins.

---

## 25. Evaluate Expression

When debugger is stopped, use:

| Mac | Windows/Linux |
|---|---|
| `Option + F8` | `Alt + F8` |

Try expressions based on your project structure.

If using DTO request:

```java
request.getTitle()
```

```java
request.getStatus()
```

If using entity:

```java
task.getTitle()
```

```java
task.getStatus()
```

Repository examples:

```java
taskRepository.count()
```

```java
taskRepository.findAll()
```

Avoid expressions that modify data unless intentional:

```java
taskRepository.deleteAll()
```

```java
taskRepository.save(...)
```

---

## 26. Watches

Watches keep important values visible while stepping.

Add watches such as:

```java
request.getTitle()
```

```java
request.getStatus()
```

or:

```java
task.getTitle()
```

```java
task.getStatus()
```

and:

```java
taskRepository.count()
```

Use the expressions that match your current project code.

---

## 27. Frames and Call Stack

The Frames panel shows how execution reached the current line.

Example flow:

```text
TaskService.createTask
TaskController.createTask
Spring MVC framework methods
Tomcat servlet methods
Thread.run
```

Important:

```text
Top frame = current method
Lower frames = methods that called it
```

Use this to understand the request path.

---

## 28. Threads View

Spring Boot handles web requests on server threads.

You may see names like:

```text
nio-8080-exec-1
nio-8080-exec-2
main
```

For this module:

```text
Focus on the thread stopped at your breakpoint.
```

You do not need advanced thread debugging yet.

---

## 29. Run to Cursor

If you want to skip several lines and stop at a specific line:

1. Put your cursor on the target line.
2. Use Run to Cursor.

| Mac | Windows/Linux |
|---|---|
| `Option + F9` | `Alt + F9` |

This is faster than pressing `F8` many times.

---

## 30. Show Execution Point

Sometimes you click around and lose the current paused line.

Use:

| Mac | Windows/Linux |
|---|---|
| `Option + F10` | `Alt + F10` |

This jumps back to the current execution line.

---

## 31. Debug Validation Errors

If your original project has validation like:

```java
@Valid @RequestBody TaskRequest request
```

and a global exception handler, test invalid input.

Example:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"","status":"OPEN"}'
```

Expected:

```text
HTTP/1.1 400
```

Set breakpoints in:

```text
Controller create method
Service validation method if available
GlobalExceptionHandler
```

Inspect:

```text
request
field errors
exception message
response body
```

If your project does not yet have validation, skip this section.

---

## 32. What To Do When You Cannot Find a Method

Use this order.

### Step 1 — Search Everywhere

```text
Shift Shift
```

Search:

```text
TaskController
```

```text
TaskService
```

```text
TaskRepository
```

### Step 2 — File Structure

Inside a Java file:

| Mac | Windows/Linux |
|---|---|
| `Cmd + F12` | `Ctrl + F12` |

Search method name:

```text
getAllTasks
createTask
updateTask
deleteTask
```

### Step 3 — Find in Files

| Mac | Windows/Linux |
|---|---|
| `Cmd + Shift + F` | `Ctrl + Shift + F` |

Search:

```text
createTask
```

```text
taskRepository.save
```

```text
@GetMapping
```

```text
@PostMapping
```

```text
@RequestMapping("/tasks")
```

---

## 33. Community Edition Replacement Table

| Original/Ultimate Style | Community Edition Method |
|---|---|
| Spring Boot Services window | Run/Debug main class |
| Spring Boot dashboard | Run tool window / Debug tool window |
| Built-in HTTP Client workflow | Terminal `curl` or Postman |
| Database tool window | H2 Console, `psql`, or DBeaver |
| Docker Services window | Docker CLI in Terminal |
| Endpoint navigation tools | Find in Files: `@GetMapping`, `@PostMapping`, `/tasks` |
| Runtime monitoring | Console logs and Terminal commands |

---

## 34. Common Debugging Issues

### Breakpoint does not hit

Check:

```text
App is running in Debug mode, not normal Run mode
Breakpoint is enabled
You called the correct URL
You used the correct HTTP method
App restarted after code changes
Correct port is used
```

### curl hangs

Usually this means:

```text
Debugger stopped at breakpoint
```

Press Resume.

### Cannot find `TaskService.createTask()`

Remember:

```text
TaskService.createTask() is not a class.
It means createTask method inside TaskService.java.
```

Open:

```text
TaskService.java
```

Then search:

```text
createTask
```

### Cannot find `taskRepository.save(task)`

Possible reasons:

```text
Your service uses a different method name
Your project is still using an in-memory list
Database module is not completed
```

Search:

```text
save(
```

or:

```text
tasks.add
```

### Step Into goes too deep into Spring code

Use:

```text
Step Out
Resume
Set breakpoint in your next class
Use Step Over next time
```

---

## 35. Final Debugging Practice

Complete this full flow:

```text
1. Start app in Debug mode.
2. Open TaskController.
3. Find the GET /tasks method.
4. Set breakpoint on the service call.
5. Run curl http://localhost:8080/tasks.
6. Confirm debugger stops.
7. Press F7 to step into service.
8. Press F8 over repository call.
9. Resume.
10. Find the POST /tasks method.
11. Set breakpoint before the service create call.
12. Run POST curl request.
13. Inspect request/task title and status.
14. Step into service create method.
15. Step over repository save.
16. Inspect saved task.
17. Check database.
18. Add conditional breakpoint for id == 999.
19. Test /tasks/1 and /tasks/999.
20. Add a logpoint.
21. Add a NullPointerException exception breakpoint.
22. Practice Evaluate Expression.
23. Add Watches.
24. Remove debug-only code.
```

---

## Module 19 Assignment

Complete these tasks:

```text
1. Open springboot-practice.
2. Start SpringbootPracticeApplication in Debug mode.
3. Open TaskController.
4. Find the GET /tasks method.
5. Set breakpoint on the service call inside GET /tasks.
6. Run curl http://localhost:8080/tasks.
7. Confirm debugger stops.
8. Step into TaskService.
9. Step over repository call.
10. Resume program.
11. Find the POST /tasks method.
12. Set breakpoint before or on the service create call.
13. Run POST /tasks using curl.
14. Inspect request/task title and status.
15. Step into TaskService create method.
16. Step over repository save call.
17. Inspect saved result if available.
18. Debug GET /tasks/1.
19. Debug GET /tasks/999.
20. Add conditional breakpoint id == 999.
21. Add logpoint in create method.
22. Add NullPointerException exception breakpoint.
23. Practice exception debugging if included in your original module.
24. Use Evaluate Expression.
25. Add Watches.
26. Review console logs.
27. Review Git diff.
28. Remove debug-only code.
29. Commit with message:
    Practice advanced debugging workflow in IntelliJ Community Edition
```

When done, reply:

```text
Module 19 completed
```
