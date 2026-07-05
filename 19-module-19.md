# Module 19 — Advanced Debugging in IntelliJ IDEA Community Edition

## Goal

In this module, you will learn how to debug your Spring Boot project in **IntelliJ IDEA Community Edition**.

This corrected version gives exact guidance to find:

```text
TaskController
TaskService
TaskRepository
getAllTasks()
getTaskById()
createTask()
updateTask()
deleteTask()
taskRepository.save(task)
```

This module uses your current simple project structure:

```java
public List<Task> getAllTasks() {
    return taskService.getAllTasks();
}
```

It does **not** use:

```java
TaskResponse
TaskMapper
```

Those are for later improvements.

---

## 1. First Understand the Debugging Flow

For a Spring Boot REST API, the flow is:

```text
curl/browser request
→ TaskController
→ TaskService
→ TaskRepository
→ Database
```

Example:

```bash
curl http://localhost:8080/tasks
```

goes through:

```text
TaskController.getAllTasks()
→ TaskService.getAllTasks()
→ TaskRepository.findAll()
→ Database
```

Example:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Debug task","status":"OPEN"}'
```

goes through:

```text
TaskController.createTask()
→ TaskService.createTask()
→ TaskRepository.save(task)
→ Database
```

---

## 2. Confirm Your Project Files

Your project should have these files:

```text
springboot-practice
 ├── pom.xml
 ├── src
 │   └── main
 │       ├── java
 │       │   └── com
 │       │       └── example
 │       │           └── springbootpractice
 │       │               ├── SpringbootPracticeApplication.java
 │       │               ├── controller
 │       │               │   └── TaskController.java
 │       │               ├── model
 │       │               │   └── Task.java
 │       │               ├── repository
 │       │               │   └── TaskRepository.java
 │       │               └── service
 │       │                   └── TaskService.java
 │       └── resources
 │           └── application.properties
```

The important files for this module are:

```text
TaskController.java
TaskService.java
TaskRepository.java
Task.java
SpringbootPracticeApplication.java
```

---

## 3. How to Find `TaskController`

Use **Search Everywhere**.

Press:

```text
Shift Shift
```

Type:

```text
TaskController
```

Open:

```text
TaskController.java
```

If you cannot find it, use **Find in Files**:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Shift + F` | `Ctrl + Shift + F` |

Search:

```text
@RequestMapping("/tasks")
```

or:

```text
@GetMapping
```

or:

```text
@PostMapping
```

If nothing appears, your controller may not exist yet.

---

## 4. `TaskController` Expected Code

Your `TaskController.java` should look similar to this:

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
    public ResponseEntity<Task> createTask(@RequestBody Task task) {
        return ResponseEntity.ok(taskService.createTask(task));
    }

    @PutMapping("/{id}")
    public ResponseEntity<Task> updateTask(@PathVariable Long id, @RequestBody Task task) {
        return taskService.updateTask(id, task)
                .map(ResponseEntity::ok)
                .orElse(ResponseEntity.notFound().build());
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteTask(@PathVariable Long id) {
        if (taskService.deleteTask(id)) {
            return ResponseEntity.noContent().build();
        }

        return ResponseEntity.notFound().build();
    }
}
```

---

## 5. How to Find Methods Inside `TaskController`

Open:

```text
TaskController.java
```

Then use **File Structure**.

| Mac | Windows/Linux |
|---|---|
| `Cmd + F12` | `Ctrl + F12` |

Search inside the popup for:

```text
getAllTasks
getTaskById
createTask
updateTask
deleteTask
```

This is the fastest way to jump to a method inside a Java file.

---

## 6. Method Map for `TaskController`

| HTTP Request | Controller Method | Search Term |
|---|---|---|
| `GET /tasks` | `getAllTasks()` | `getAllTasks` |
| `GET /tasks/{id}` | `getTaskById(Long id)` | `getTaskById` |
| `POST /tasks` | `createTask(Task task)` | `createTask` |
| `PUT /tasks/{id}` | `updateTask(Long id, Task task)` | `updateTask` |
| `DELETE /tasks/{id}` | `deleteTask(Long id)` | `deleteTask` |

---

## 7. How to Find `getAllTasks()`

Inside `TaskController.java`, press:

```text
Cmd + F12
```

or:

```text
Ctrl + F12
```

Search:

```text
getAllTasks
```

You should find:

```java
@GetMapping
public List<Task> getAllTasks() {
    return taskService.getAllTasks();
}
```

Set your breakpoint on this line:

```java
return taskService.getAllTasks();
```

This breakpoint is used when you call:

```bash
curl http://localhost:8080/tasks
```

---

## 8. How to Find `createTask()`

Inside `TaskController.java`, press:

```text
Cmd + F12
```

or:

```text
Ctrl + F12
```

Search:

```text
createTask
```

You should find:

```java
@PostMapping
public ResponseEntity<Task> createTask(@RequestBody Task task) {
    return ResponseEntity.ok(taskService.createTask(task));
}
```

Set your breakpoint on this line:

```java
return ResponseEntity.ok(taskService.createTask(task));
```

This breakpoint is used when you call:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Advanced debugging task","status":"OPEN"}'
```

---

## 9. How to Find `TaskService`

Use **Search Everywhere**.

Press:

```text
Shift Shift
```

Type:

```text
TaskService
```

Open:

```text
TaskService.java
```

If you cannot find it, use Find in Files:

```text
taskRepository
```

or:

```text
public List<Task> getAllTasks
```

or:

```text
public Task createTask
```

---

## 10. `TaskService` Expected Code

If you completed the database module, `TaskService.java` should look similar to this:

```java
package com.example.springbootpractice.service;

import com.example.springbootpractice.model.Task;
import com.example.springbootpractice.repository.TaskRepository;
import org.springframework.stereotype.Service;

import java.util.List;
import java.util.Optional;

@Service
public class TaskService {

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
        return taskRepository.save(task);
    }

    public Optional<Task> updateTask(Long id, Task updatedTask) {
        return taskRepository.findById(id)
                .map(existingTask -> {
                    existingTask.setTitle(updatedTask.getTitle());
                    existingTask.setStatus(updatedTask.getStatus());
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

---

## 11. If Your `TaskService` Is Still In-Memory

Your `createTask()` may look like this:

```java
public Task createTask(Task task) {
    task.setId(nextId++);
    tasks.add(task);
    return task;
}
```

That means you are still using the older in-memory version.

For debugging practice, that is okay.

Use breakpoint on:

```java
tasks.add(task);
```

But if you are doing database debugging, your method should be:

```java
public Task createTask(Task task) {
    return taskRepository.save(task);
}
```

Use breakpoint on:

```java
return taskRepository.save(task);
```

---

## 12. How to Find `createTask()` in `TaskService`

Open:

```text
TaskService.java
```

Press:

```text
Cmd + F12
```

or:

```text
Ctrl + F12
```

Search:

```text
createTask
```

You should find one of these versions.

Database version:

```java
public Task createTask(Task task) {
    return taskRepository.save(task);
}
```

In-memory version:

```java
public Task createTask(Task task) {
    task.setId(nextId++);
    tasks.add(task);
    return task;
}
```

---

## 13. How to Find `TaskRepository`

Press:

```text
Shift Shift
```

Type:

```text
TaskRepository
```

Open:

```text
TaskRepository.java
```

Expected code:

```java
package com.example.springbootpractice.repository;

import com.example.springbootpractice.model.Task;
import org.springframework.data.jpa.repository.JpaRepository;

public interface TaskRepository extends JpaRepository<Task, Long> {
}
```

This file does not show `save()`, `findAll()`, or `findById()` directly because they come from:

```java
JpaRepository<Task, Long>
```

That is why this line in `TaskService` works:

```java
return taskRepository.save(task);
```

---

## 14. How to Start Debug Mode

Open:

```text
SpringbootPracticeApplication.java
```

Click the **bug icon** near the `main()` method.

Or use:

| Mac | Windows/Linux |
|---|---|
| `Ctrl + D` | `Shift + F9` |

Expected log:

```text
Tomcat started on port 8080
Started SpringbootPracticeApplication
```

Now your app is running in Debug mode.

---

## 15. Debugging Shortcuts

| Action | Mac | Windows/Linux |
|---|---|---|
| Start Debug | `Ctrl + D` | `Shift + F9` |
| Toggle Breakpoint | `Cmd + F8` | `Ctrl + F8` |
| Step Over | `F8` | `F8` |
| Step Into | `F7` | `F7` |
| Step Out | `Shift + F8` | `Shift + F8` |
| Resume Program | `Cmd + Option + R` | `F9` |
| Evaluate Expression | `Option + F8` | `Alt + F8` |
| View Breakpoints | `Cmd + Shift + F8` | `Ctrl + Shift + F8` |
| Stop Debugging | `Cmd + F2` | `Ctrl + F2` |

If a shortcut does not work:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Shift + A` | `Ctrl + Shift + A` |

Then search the action name.

---

## 16. Debug `GET /tasks`

Open:

```text
TaskController.java
```

Find:

```java
@GetMapping
public List<Task> getAllTasks() {
    return taskService.getAllTasks();
}
```

Set breakpoint on:

```java
return taskService.getAllTasks();
```

Run this in Terminal:

```bash
curl http://localhost:8080/tasks
```

Expected:

```text
Debugger stops at TaskController.getAllTasks()
curl waits
```

Now press:

```text
F7
```

This steps into:

```java
public List<Task> getAllTasks() {
    return taskRepository.findAll();
}
```

Now you are inside `TaskService`.

At:

```java
return taskRepository.findAll();
```

press:

```text
F8
```

This steps over the repository call.

Then press Resume:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Option + R` | `F9` |

Now curl should return JSON.

---

## 17. Debug `POST /tasks`

Open:

```text
TaskController.java
```

Find:

```java
@PostMapping
public ResponseEntity<Task> createTask(@RequestBody Task task) {
    return ResponseEntity.ok(taskService.createTask(task));
}
```

Set breakpoint on:

```java
return ResponseEntity.ok(taskService.createTask(task));
```

Run:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Advanced debugging task","status":"OPEN"}'
```

Debugger stops in:

```text
TaskController.createTask()
```

Inspect:

```text
task
task.id
task.title
task.status
```

If you cannot see private fields clearly, use Evaluate Expression:

```java
task.getTitle()
```

```java
task.getStatus()
```

Expected:

```text
Advanced debugging task
OPEN
```

---

## 18. Step from Controller to Service

When stopped at:

```java
return ResponseEntity.ok(taskService.createTask(task));
```

Put your cursor on:

```text
taskService.createTask(task)
```

Press:

```text
F7
```

You should enter:

```java
public Task createTask(Task task) {
    return taskRepository.save(task);
}
```

Now you are inside:

```text
TaskService.createTask()
```

Set a breakpoint on:

```java
return taskRepository.save(task);
```

Then press:

```text
F8
```

This saves the task.

---

## 19. Easier Debug Version of `createTask()`

For learning, this version is easier to debug:

```java
public Task createTask(Task task) {
    Task savedTask = taskRepository.save(task);
    return savedTask;
}
```

Now set breakpoint on:

```java
return savedTask;
```

Inspect:

```text
savedTask.id
savedTask.title
savedTask.status
```

This helps you clearly see the saved object after database save.

---

## 20. Debug `GET /tasks/{id}`

Open:

```text
TaskController.java
```

Find:

```java
@GetMapping("/{id}")
public ResponseEntity<Task> getTaskById(@PathVariable Long id) {
    return taskService.getTaskById(id)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
}
```

Set breakpoint on:

```java
return taskService.getTaskById(id)
```

Run:

```bash
curl -i http://localhost:8080/tasks/1
```

Inspect:

```text
id
```

Press `F7`.

You should enter:

```java
public Optional<Task> getTaskById(Long id) {
    return taskRepository.findById(id);
}
```

Use `F8` on:

```java
return taskRepository.findById(id);
```

---

## 21. Debug 404 Flow

Run:

```bash
curl -i http://localhost:8080/tasks/999
```

Expected:

```text
HTTP/1.1 404
```

Breakpoints:

```text
TaskController.getTaskById()
TaskService.getTaskById()
```

Inspect:

```text
id = 999
Optional is empty
ResponseEntity.notFound()
```

This teaches you how a missing record becomes HTTP 404.

---

## 22. Debug `PUT /tasks/{id}`

Open:

```text
TaskController.java
```

Find:

```java
@PutMapping("/{id}")
public ResponseEntity<Task> updateTask(@PathVariable Long id, @RequestBody Task task) {
    return taskService.updateTask(id, task)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
}
```

Set breakpoint on:

```java
return taskService.updateTask(id, task)
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
task.title
task.status
```

Step into `TaskService.updateTask()`.

---

## 23. Debug `DELETE /tasks/{id}`

Open:

```text
TaskController.java
```

Find:

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
if (taskService.deleteTask(id)) {
```

Run:

```bash
curl -i -X DELETE http://localhost:8080/tasks/1
```

Inspect:

```text
id
```

Step into:

```java
public boolean deleteTask(Long id) {
    if (!taskRepository.existsById(id)) {
        return false;
    }

    taskRepository.deleteById(id);
    return true;
}
```

---

## 24. Conditional Breakpoint

A conditional breakpoint stops only when a condition is true.

Example:

In `TaskController.getTaskById()`, set breakpoint on:

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

Debugger should not stop.

Run:

```bash
curl http://localhost:8080/tasks/999
```

Debugger should stop.

---

## 25. Useful Conditional Breakpoints

Use these:

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
task.getStatus() == null
```

```java
task.getStatus().equals("COMPLETED")
```

Safer version:

```java
"COMPLETED".equals(task.getStatus())
```

---

## 26. Logpoints

A logpoint prints a message without stopping the app.

Set breakpoint in:

```text
TaskService.createTask()
```

Right-click the breakpoint.

Change:

```text
Uncheck Suspend
Enable Log message to console
```

Message:

```text
createTask method called
```

Run:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Logpoint test","status":"OPEN"}'
```

Expected:

```text
App does not pause
Message appears in debug console
```

---

## 27. Exception Breakpoint

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

Now IntelliJ will stop when a `NullPointerException` happens.

---

## 28. Practice Exception Debugging

Create:

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

Debugger should stop on:

```java
return value.toUpperCase();
```

After practice, delete this file or keep it only on a learning branch.

---

## 29. Evaluate Expression

When stopped at a breakpoint, use:

| Mac | Windows/Linux |
|---|---|
| `Option + F8` | `Alt + F8` |

Try:

```java
task.getTitle()
```

```java
task.getStatus()
```

```java
taskRepository.count()
```

```java
taskRepository.findAll()
```

Avoid dangerous expressions like:

```java
taskRepository.deleteAll()
```

because that changes data.

---

## 30. Watches

In the Debug window, add Watches:

```java
task.getTitle()
```

```java
task.getStatus()
```

```java
taskRepository.count()
```

Watches keep important values visible while stepping through code.

---

## 31. Check Database After Debugging

If using H2:

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

Then:

```sql
SELECT * FROM task;
```

Confirm the task you created is saved.

---

## 32. What to Do When You Cannot Find a Method

Use this exact fallback order:

### Step 1 — Search Everywhere

```text
Shift Shift
```

Search:

```text
TaskController
```

or:

```text
TaskService
```

### Step 2 — File Structure

Inside the file:

```text
Cmd + F12
```

or:

```text
Ctrl + F12
```

Search:

```text
createTask
```

### Step 3 — Find in Files

```text
Cmd + Shift + F
```

or:

```text
Ctrl + Shift + F
```

Search:

```text
createTask
```

or:

```text
taskRepository.save
```

or:

```text
@PostMapping
```

### Step 4 — Search by endpoint annotation

Search:

```text
@GetMapping
```

```text
@PostMapping
```

```text
@PutMapping
```

```text
@DeleteMapping
```

```text
@RequestMapping("/tasks")
```

---

## 33. Method Search Table

| What You Need | Search This | File |
|---|---|---|
| All tasks endpoint | `getAllTasks` | `TaskController.java` |
| Create task endpoint | `createTask` | `TaskController.java` |
| Save logic | `taskRepository.save` | `TaskService.java` |
| Find all DB logic | `taskRepository.findAll` | `TaskService.java` |
| Find by ID logic | `taskRepository.findById` | `TaskService.java` |
| Delete logic | `deleteTask` | `TaskService.java` |
| REST mappings | `@GetMapping`, `@PostMapping` | `TaskController.java` |
| Base route | `@RequestMapping("/tasks")` | `TaskController.java` |

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

### Cannot find `taskRepository.save(task)`

Possible reasons:

```text
You are still using in-memory TaskService
Database module is not completed
TaskService has different method name
```

Search:

```text
save(
```

or:

```text
tasks.add
```

### Cannot find `getAllTasks()`

Search:

```text
@GetMapping
```

or:

```text
findAll
```

or:

```text
/tasks
```

---

## 35. Final Debugging Practice

Complete this full flow:

```text
1. Start app in Debug mode.
2. Open TaskController.
3. Find getAllTasks using Cmd/Ctrl + F12.
4. Set breakpoint on return taskService.getAllTasks().
5. Run curl http://localhost:8080/tasks.
6. Confirm debugger stops.
7. Press F7 to step into TaskService.
8. Press F8 over taskRepository.findAll().
9. Resume.
10. Find createTask in TaskController.
11. Set breakpoint on taskService.createTask(task).
12. Run POST curl request.
13. Inspect task.title and task.status.
14. Step into TaskService.createTask.
15. Step over taskRepository.save(task).
16. Inspect saved task.
17. Check database.
18. Add conditional breakpoint for id == 999.
19. Test /tasks/1 and /tasks/999.
20. Add a logpoint.
21. Add a NullPointerException exception breakpoint.
22. Practice Evaluate Expression.
23. Add Watches.
```

---

## Module 19 Assignment

Complete these tasks:

```text
1. Open springboot-practice.
2. Press Shift Shift and open TaskController.
3. Use Cmd/Ctrl + F12 to find getAllTasks.
4. Set breakpoint on return taskService.getAllTasks().
5. Start SpringbootPracticeApplication in Debug mode.
6. Run curl http://localhost:8080/tasks.
7. Confirm debugger stops.
8. Step into TaskService.getAllTasks.
9. Step over taskRepository.findAll.
10. Resume program.
11. Use Cmd/Ctrl + F12 to find createTask in TaskController.
12. Set breakpoint on taskService.createTask(task).
13. Run POST /tasks using curl.
14. Inspect task title and status.
15. Step into TaskService.createTask.
16. Find taskRepository.save(task).
17. Step over taskRepository.save(task).
18. Inspect saved task.
19. Use Shift Shift to open TaskRepository.
20. Confirm it extends JpaRepository<Task, Long>.
21. Debug GET /tasks/1.
22. Debug GET /tasks/999.
23. Add conditional breakpoint id == 999.
24. Add logpoint in createTask.
25. Add NullPointerException exception breakpoint.
26. Create DebugErrorController.
27. Call /debug/error.
28. Confirm debugger stops.
29. Use Evaluate Expression.
30. Add Watches.
31. Review Git diff.
32. Remove DebugErrorController or commit it only as practice code.
33. Commit with message:
    Practice advanced debugging workflow in IntelliJ Community Edition
```

When done, reply:

```text
Module 19 completed
```
