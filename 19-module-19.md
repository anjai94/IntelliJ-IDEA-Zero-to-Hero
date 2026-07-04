# Module 19 — Advanced Debugging in IntelliJ IDEA Community Edition

## Goal

In this module, you will learn advanced debugging techniques using **IntelliJ IDEA Community Edition**.

Because you are using **Community Edition**, we will not depend on Ultimate-only Spring debugging features. Instead, we will use the standard IntelliJ Java debugger, which is fully powerful enough for real Spring Boot debugging.

You will learn:

```text
Debugging Spring Boot as a normal Java app
Breakpoints
Conditional breakpoints
Logpoints
Exception breakpoints
Evaluate Expression
Watches
Frames / call stack
Thread view
Debugging GET requests
Debugging POST requests
Debugging validation errors
Debugging database save flow
Reading stack traces
Common debugger issues
```

---

## 1. Community Edition Debugging Mindset

In Community Edition, Spring Boot runs as a normal Java application.

That means this class is your starting point:

```text
SpringbootPracticeApplication
```

You can debug it the same way you debug any Java `main()` method.

The flow is:

```text
Start app in Debug mode
Send request using curl/browser/Postman
Debugger stops at breakpoint
Inspect variables
Step through controller → service → repository
Resume app
```

This is enough for most real debugging work.

---

## 2. Project Used in This Module

Use your project:

```text
springboot-practice
```

Expected packages:

```text
com.example.springbootpractice
 ├── controller
 ├── service
 ├── repository
 ├── model
 ├── dto
 ├── mapper
 ├── exception
 └── config
```

Important files:

```text
SpringbootPracticeApplication.java
TaskController.java
TaskService.java
TaskRepository.java
Task.java
GlobalExceptionHandler.java
```

If your project structure is slightly different, follow the same concepts using your actual class names.

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
| Run to Cursor | `Option + F9` | `Alt + F9` |
| Evaluate Expression | `Option + F8` | `Alt + F8` |
| Show Execution Point | `Option + F10` | `Alt + F10` |
| Stop Debugging | `Cmd + F2` | `Ctrl + F2` |

If a shortcut does not work, use:

| Action | Mac | Windows/Linux |
|---|---|---|
| Find Action | `Cmd + Shift + A` | `Ctrl + Shift + A` |

Search the action name, for example:

```text
Evaluate Expression
View Breakpoints
Run to Cursor
Show Execution Point
```

---

## 4. Start Spring Boot in Debug Mode

Open:

```text
SpringbootPracticeApplication.java
```

Click the bug icon near the `main()` method, or use:

| Mac | Windows/Linux |
|---|---|
| `Ctrl + D` | `Shift + F9` |

Expected log:

```text
Tomcat started on port 8080
Started SpringbootPracticeApplication
```

You are now running the app in Debug mode.

---

## 5. Debug GET `/tasks`

Open:

```text
TaskController.java
```

Find:

```java
@GetMapping
public List<TaskResponse> getAllTasks() {
    return taskService.getAllTasks()
            .stream()
            .map(taskMapper::toResponse)
            .toList();
}
```

Set a breakpoint on this line:

```java
return taskService.getAllTasks()
```

Now send request from IntelliJ Terminal:

```bash
curl http://localhost:8080/tasks
```

The debugger should stop at the breakpoint.

---

## 6. Inspect Variables

When debugger stops, look at the Debug window.

Important areas:

```text
Frames
Variables
Watches
Console
Threads
```

In `TaskController.getAllTasks`, inspect:

```text
this
taskService
taskMapper
```

If you have response variables, inspect:

```text
tasks
task responses
```

---

## 7. Step Into Service Layer

When stopped at:

```java
return taskService.getAllTasks()
```

Press:

```text
F7
```

This is **Step Into**.

It should move into:

```text
TaskService.getAllTasks
```

Example:

```java
public List<Task> getAllTasks() {
    return taskRepository.findAll();
}
```

Now you can see the service layer.

---

## 8. Step Over Repository Call

When inside:

```java
return taskRepository.findAll();
```

Press:

```text
F8
```

This is **Step Over**.

It executes the repository call without going deep into Spring Data JPA internals.

Important rule:

```text
Step Into your own code.
Step Over framework/library code unless you really need to inspect it.
```

---

## 9. Resume Program

After inspecting, continue execution:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Option + R` | `F9` |

The curl request should complete and return JSON.

---

## 10. Debug POST `/tasks`

Set breakpoints in:

```text
TaskController.createTask
TaskService.createTask
TaskRepository.save line
```

Example controller method:

```java
@PostMapping
public ResponseEntity<TaskResponse> createTask(@Valid @RequestBody TaskRequest request) {
    Task task = taskMapper.toEntity(request);
    Task createdTask = taskService.createTask(task);
    return ResponseEntity.ok(taskMapper.toResponse(createdTask));
}
```

Set breakpoints on:

```java
Task task = taskMapper.toEntity(request);
Task createdTask = taskService.createTask(task);
return ResponseEntity.ok(taskMapper.toResponse(createdTask));
```

Send request:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Advanced debugging task","status":"OPEN"}'
```

Debugger should stop in `createTask`.

---

## 11. Inspect POST Request Body

When debugger stops, inspect:

```text
request
request.title
request.status
```

If your DTO has getters, use Evaluate Expression:

```java
request.getTitle()
request.getStatus()
```

Expected:

```text
Advanced debugging task
OPEN
```

---

## 12. Step Through Mapper

At:

```java
Task task = taskMapper.toEntity(request);
```

Press:

```text
F7
```

You should enter:

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
request
task
task.title
task.status
```

Then press `Shift + F8` to Step Out back to the controller.

---

## 13. Step Into Service Create

At:

```java
Task createdTask = taskService.createTask(task);
```

Press:

```text
F7
```

You should enter:

```java
public Task createTask(Task task) {
    applyDefaultStatusIfMissing(task);
    return taskRepository.save(task);
}
```

or your current version.

Inspect:

```text
task.title
task.status
```

---

## 14. Debug Default Status Logic

If your service has this logic:

```java
private String resolveStatus(String status) {
    if (status == null || status.isBlank()) {
        return DEFAULT_STATUS;
    }

    return status;
}
```

Send request without status:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Task without status"}'
```

Set breakpoint inside `resolveStatus`.

Inspect:

```text
status
DEFAULT_STATUS
```

Expected:

```text
status = null
DEFAULT_STATUS = OPEN
```

Final saved task should have:

```text
status = OPEN
```

---

## 15. Debug Database Save

At:

```java
return taskRepository.save(task);
```

Use **Step Over** instead of Step Into.

Reason:

```text
taskRepository.save is Spring Data JPA framework code.
Usually you only need to inspect before and after the call.
```

After Step Over, inspect:

```text
createdTask.id
createdTask.title
createdTask.status
```

If the ID is generated, it should now have a value.

---

## 16. Check Database After Debugging

If using H2 Console:

```text
http://localhost:8080/h2-console
```

SQL:

```sql
SELECT * FROM TASK;
```

If using PostgreSQL Docker:

```bash
docker exec -it task-postgres psql -U taskuser -d taskdb
```

Then:

```sql
SELECT * FROM task;
```

Expected: the task you created during debugging should be visible.

---

## 17. Conditional Breakpoints

A conditional breakpoint only stops when a condition is true.

Open:

```text
TaskController.java
```

Find:

```java
@GetMapping("/{id}")
public ResponseEntity<TaskResponse> getTaskById(@PathVariable Long id) {
    return taskService.getTaskById(id)
            .map(taskMapper::toResponse)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
}
```

Set a breakpoint on:

```java
return taskService.getTaskById(id)
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

Debugger should **not** stop.

Run:

```bash
curl http://localhost:8080/tasks/999
```

Debugger should stop.

This is useful when a method is called many times and you only care about one case.

---

## 18. Conditional Breakpoint Examples

Useful conditions:

```java
id == 1
```

```java
id > 100
```

```java
request.getTitle().contains("debug")
```

```java
task.getStatus() == null
```

```java
task.getTitle() == null || task.getTitle().isBlank()
```

Be careful: if the condition itself throws an exception, the debugger may show an error.

---

## 19. Logpoints

A logpoint prints a message without stopping the application.

This is useful when:

```text
You want to observe values
You do not want to pause execution
The endpoint is called many times
You want temporary debug logging without changing code
```

### Create Logpoint

Set breakpoint in:

```text
TaskService.createTask
```

Right-click breakpoint.

Change settings:

```text
Uncheck Suspend
Enable Log message to console
```

Example message:

```text
Creating task in service
```

If expression logging is available in your version, try:

```text
Creating task: {task.getTitle()}
```

If expression logging does not work well, keep it simple.

Send request:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Logpoint test","status":"OPEN"}'
```

Expected: app does not pause, but a message appears in debugger console.

---

## 20. Exception Breakpoints

Exception breakpoints stop the debugger when a specific exception is thrown.

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

Now the debugger can stop when a `NullPointerException` occurs.

---

## 21. Create Debug Error Controller

Create class:

```text
controller/DebugErrorController.java
```

Paste:

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

Expected: debugger stops where the `NullPointerException` occurs.

Important: this class is for practice only. Remove it before final production-style commit, or keep it only on a learning branch.

---

## 22. Read the Stack Trace

When an exception happens, look for your package:

```text
com.example.springbootpractice
```

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

## 23. Evaluate Expression

When debugger is stopped, use:

| Mac | Windows/Linux |
|---|---|
| `Option + F8` | `Alt + F8` |

Try expressions like:

```java
request.getTitle()
```

```java
request.getStatus()
```

```java
task.getTitle().toUpperCase()
```

```java
taskRepository.count()
```

```java
taskRepository.findAll()
```

Be careful with expressions that modify data.

Avoid evaluating:

```java
taskRepository.deleteAll()
taskRepository.save(...)
```

unless you intentionally want to change data.

---

## 24. Watches

Watches let you keep important expressions visible.

In Debug window, add watches:

```java
request.getTitle()
request.getStatus()
task.getTitle()
task.getStatus()
taskRepository.count()
```

Watches are useful when stepping through multiple lines and you want values visible all the time.

---

## 25. Frames and Call Stack

The Frames panel shows how execution reached the current line.

Example flow:

```text
TaskService.createTask
TaskController.createTask
Spring MVC framework methods
Tomcat servlet methods
Thread.run
```

Use frames to move between caller and callee.

Important:

```text
Top frame = current method
Lower frames = methods that called it
```

This helps you understand request flow.

---

## 26. Threads View

Spring Boot handles web requests on server threads.

You may see names like:

```text
nio-8080-exec-1
nio-8080-exec-2
main
```

For beginner/intermediate debugging:

```text
Focus on the thread that is stopped at your breakpoint.
```

You do not need advanced thread debugging yet unless you are investigating concurrency issues.

---

## 27. Run to Cursor

If you want to skip several lines and stop at a specific line:

1. Put your cursor on the target line
2. Use Run to Cursor

| Mac | Windows/Linux |
|---|---|
| `Option + F9` | `Alt + F9` |

This is faster than pressing `F8` many times.

---

## 28. Show Execution Point

Sometimes you click around and lose the current paused line.

Use:

| Mac | Windows/Linux |
|---|---|
| `Option + F10` | `Alt + F10` |

This jumps back to the current execution line.

---

## 29. Debug Validation Error

If you completed Module 26-style validation or added validation earlier, test invalid request:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"","status":"OPEN"}'
```

Expected:

```text
HTTP/1.1 400
```

Set breakpoint in:

```text
GlobalExceptionHandler.handleValidationException
```

Run invalid request again.

Inspect:

```text
exception
exception.getBindingResult()
field errors
error message
```

This teaches how validation errors are handled.

---

## 30. Debug 404 Not Found Flow

Call:

```bash
curl -i http://localhost:8080/tasks/999
```

Set breakpoint in:

```text
TaskController.getTaskById
TaskService.getTaskById
```

Inspect:

```text
id
Optional result
ResponseEntity.notFound()
```

Expected:

```text
HTTP/1.1 404
```

This helps you understand normal “not found” behavior.

---

## 31. Debug DELETE Flow

Set breakpoint in:

```text
TaskController.deleteTask
TaskService.deleteTask
```

Call:

```bash
curl -i -X DELETE http://localhost:8080/tasks/1
```

Inspect:

```text
id
existsById result
deleteById call
boolean deleted
```

Then call again:

```bash
curl -i -X DELETE http://localhost:8080/tasks/1
```

Expected second call may return:

```text
HTTP/1.1 404
```

because the task was already deleted.

---

## 32. Debug PUT Flow

Set breakpoint in:

```text
TaskController.updateTask
TaskService.updateTask
```

Call:

```bash
curl -i -X PUT http://localhost:8080/tasks/1 \
  -H "Content-Type: application/json" \
  -d '{"title":"Updated during debugging","status":"COMPLETED"}'
```

Inspect:

```text
id
request title
request status
existingTask
updatedTask
saved task
```

This is useful for understanding update behavior.

---

## 33. Debugging with Different Ports

If your app runs on port 8081:

```bash
curl http://localhost:8081/tasks
```

Make sure curl uses the same port as the app log.

Check startup log:

```text
Tomcat started on port 8081
```

Common mistake:

```text
App is running on 8081 but request is sent to 8080.
```

---

## 34. Debugging with PostgreSQL Docker

If Module 18 is completed and you use PostgreSQL Docker:

1. Start PostgreSQL:

```bash
docker compose up -d
```

2. Run app in Debug mode.

3. Send POST request:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"PostgreSQL debug task","status":"OPEN"}'
```

4. Step through controller and service.

5. Check database:

```bash
docker exec -it task-postgres psql -U taskuser -d taskdb
```

```sql
SELECT * FROM task;
```

This proves that the debugger and database flow are connected.

---

## 35. Do Not Debug Too Deep into Framework Code

Sometimes Step Into takes you into:

```text
Spring Framework classes
Hibernate classes
JDK proxy classes
Tomcat classes
Reflection code
```

If this happens:

- Use Step Out
- Use Resume
- Set breakpoint in your next class
- Step Over framework calls next time

Rule:

```text
Debug your code first.
Only debug framework code when necessary.
```

---

## 36. Temporary Debug Code

Avoid leaving temporary debug code like:

```java
System.out.println("debug here");
```

or:

```java
DebugErrorController
```

in final commits.

Before committing, search:

```text
debug
System.out.println
TODO
temporary
test only
```

Use Find in Files:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Shift + F` | `Ctrl + Shift + F` |

---

## 37. Common Debugger Issues

### Issue 1 — Breakpoint Does Not Hit

Check:

```text
App is running in Debug mode, not Run mode
Breakpoint is enabled
Request URL is correct
Request method is correct: GET/POST/PUT/DELETE
Code path is actually executed
App was restarted after code changes
```

### Issue 2 — curl Hangs

Possible reason:

```text
Debugger stopped at breakpoint and request is waiting
```

Resume the program.

### Issue 3 — Values Look Old

Check:

```text
You restarted the app after code changes
You are hitting the correct port
You are not running two app instances
Database contains old data
```

### Issue 4 — Step Into Goes Too Deep

Use:

```text
Step Out
Resume
Set breakpoint in your next class
Use Step Over next time
```

### Issue 5 — Conditional Breakpoint Fails

Check:

```text
Condition uses correct variable name
Variable is available on that line
Condition does not cause NullPointerException
Condition syntax is valid Java
```

### Issue 6 — App Stops on Too Many Exceptions

If exception breakpoint is too broad, disable it.

Open:

```text
View Breakpoints
```

Uncheck the exception breakpoint.

---

## 38. Advanced Debugging Workflow

Use this workflow for real issues:

```text
1. Reproduce the issue with curl/browser/Postman
2. Find the controller method
3. Add breakpoint in controller
4. Start app in Debug mode
5. Send request again
6. Inspect request values
7. Step into service
8. Step over repository/framework calls
9. Inspect result/response
10. Check database if needed
11. Add conditional breakpoint if too many calls
12. Add exception breakpoint for unexpected exceptions
13. Fix code
14. Retest request
15. Review Git diff
```

---

## 39. Community Edition Important Note

In IntelliJ IDEA Ultimate, there may be extra Spring-specific tools.

In Community Edition, use:

| Need | Community Edition Method |
|---|---|
| Debug Spring Boot | Debug main class |
| Test endpoint | curl/browser/Postman |
| Inspect request body | Breakpoint in controller |
| Inspect business logic | Breakpoint in service |
| Inspect database save | Step over repository + check DB |
| Debug validation | Breakpoint in exception handler |
| Find endpoint | Search annotations/path |
| Debug 404 | Breakpoint in controller/service |
| Debug Docker DB | Docker CLI + psql |

This is a complete and practical workflow.

---

## 40. Final Check

Before completing this module, confirm:

```text
You can start Spring Boot in Debug mode
You can debug GET /tasks
You can debug POST /tasks
You can inspect request DTO values
You can step into mapper/service
You can step over repository calls
You can use conditional breakpoints
You can use logpoints
You can use exception breakpoints
You can use Evaluate Expression
You can add Watches
You can read Frames/call stack
You can debug validation error flow
You can debug 404 flow
You can debug database save behavior
```

---

## Module 19 Assignment

Complete these tasks:

```text
1. Open springboot-practice
2. Start SpringbootPracticeApplication in Debug mode
3. Set breakpoint in TaskController.getAllTasks
4. Run curl http://localhost:8080/tasks
5. Confirm debugger stops
6. Step into TaskService.getAllTasks
7. Step over repository call
8. Resume program
9. Set breakpoint in TaskController.createTask
10. Set breakpoint in TaskService.createTask
11. Send POST /tasks using curl
12. Inspect request title and status
13. Step into TaskMapper.toEntity if available
14. Step into TaskService.createTask
15. Step over taskRepository.save
16. Inspect saved task id
17. Add conditional breakpoint for id == 999 in getTaskById
18. Test /tasks/1 and /tasks/999
19. Add logpoint in createTask
20. Add NullPointerException exception breakpoint
21. Create DebugErrorController
22. Call /debug/error
23. Confirm debugger stops on exception
24. Use Evaluate Expression
25. Add at least two Watches
26. Debug invalid POST request if validation exists
27. Debug 404 not found flow
28. Debug PUT or DELETE flow
29. Remove or commit separately any debug-only code
30. Review Git diff
31. Commit with message:
    Practice advanced debugging workflows
```

When done, reply:

```text
Module 19 completed
```
