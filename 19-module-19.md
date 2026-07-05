# Module 19 — Advanced Debugging in IntelliJ IDEA Community Edition  
## Database Version Only

## Goal

In this module, you will learn advanced debugging in **IntelliJ IDEA Community Edition** using the **database-backed Spring Boot version** of the project.

This module assumes you are using:

```text
TaskController
→ TaskService
→ TaskRepository
→ Database
```

This module does **not** use the older in-memory version.

Do not use:

```java
tasks.add(task);
nextId++;
```

For this module, your service layer must use:

```java
taskRepository.findAll()
taskRepository.findById(id)
taskRepository.save(task)
taskRepository.existsById(id)
taskRepository.deleteById(id)
```

---

## 1. What You Will Learn

You will learn how to debug:

```text
GET /tasks
GET /tasks/{id}
POST /tasks
PUT /tasks/{id}
DELETE /tasks/{id}
Database save flow
Repository calls
Conditional breakpoints
Logpoints
Exception breakpoints
Evaluate Expression
Watches
Call stack / Frames
```

Community Edition replacement:

```text
No Spring Boot Services window
No Ultimate Spring dashboard
Use Run/Debug main class
Use Terminal + curl
Use H2 Console, psql, or DBeaver for database checking
```

---

## 2. Expected Project Structure

Your project should look similar to this:

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

Important files for this module:

```text
SpringbootPracticeApplication.java
TaskController.java
TaskService.java
TaskRepository.java
Task.java
application.properties
```

---

## 3. Expected `TaskRepository`

Open `TaskRepository.java`.

Path:

```text
src/main/java/com/example/springbootpractice/repository/TaskRepository.java
```

It should look like this:

```java
package com.example.springbootpractice.repository;

import com.example.springbootpractice.model.Task;
import org.springframework.data.jpa.repository.JpaRepository;

public interface TaskRepository extends JpaRepository<Task, Long> {
}
```

`JpaRepository<Task, Long>` gives your project database methods such as:

```text
findAll()
findById()
save()
existsById()
deleteById()
```

You will not see these methods written inside `TaskRepository.java` because Spring Data JPA provides them automatically.

---

## 4. Expected `TaskService` — Database Version

Open `TaskService.java`.

Path:

```text
src/main/java/com/example/springbootpractice/service/TaskService.java
```

Use `Shift Shift` and search:

```text
TaskService
```

Your database-backed service should look similar to this:

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

For this module, the important database save line is:

```java
return taskRepository.save(task);
```

---

## 5. Expected `TaskController`

Open `TaskController.java`.

Path:

```text
src/main/java/com/example/springbootpractice/controller/TaskController.java
```

Use:

```text
Shift Shift → TaskController
```

Your controller should look similar to this:

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

## 6. How to Find Methods in IntelliJ Community Edition

Open `TaskController.java` or `TaskService.java`.

Use **File Structure**:

| Mac | Windows/Linux |
|---|---|
| `Cmd + F12` | `Ctrl + F12` |

Search method names:

```text
getAllTasks
getTaskById
createTask
updateTask
deleteTask
```

If you cannot find a method, use **Find in Files**:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Shift + F` | `Ctrl + Shift + F` |

Search:

```text
createTask
taskRepository.save
taskRepository.findAll
taskRepository.findById
taskRepository.existsById
taskRepository.deleteById
@GetMapping
@PostMapping
@PutMapping
@DeleteMapping
@RequestMapping("/tasks")
```

---

## 7. Debugging Shortcuts

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

If a shortcut does not work, use **Find Action**:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Shift + A` | `Ctrl + Shift + A` |

Search the action name, for example:

```text
Evaluate Expression
View Breakpoints
Run to Cursor
Show Execution Point
```

---

## 8. Start Spring Boot in Debug Mode

Open:

```text
SpringbootPracticeApplication.java
```

Click the **bug icon** beside the `main()` method.

Or use:

| Mac | Windows/Linux |
|---|---|
| `Ctrl + D` | `Shift + F9` |

Expected log:

```text
Tomcat started on port 8080
Started SpringbootPracticeApplication
```

Now the application is running in Debug mode.

---

## 9. Debug Flow: GET `/tasks`

Request:

```bash
curl http://localhost:8080/tasks
```

Expected backend flow:

```text
TaskController.getAllTasks()
→ TaskService.getAllTasks()
→ TaskRepository.findAll()
→ Database
```

Open `TaskController.java`.

Find:

```java
@GetMapping
public List<Task> getAllTasks() {
    return taskService.getAllTasks();
}
```

Set a breakpoint on:

```java
return taskService.getAllTasks();
```

Run:

```bash
curl http://localhost:8080/tasks
```

Expected:

```text
Debugger stops at TaskController.getAllTasks()
curl waits until you resume
```

Press:

```text
F7
```

This steps into `TaskService.getAllTasks()`.

You should reach:

```java
public List<Task> getAllTasks() {
    return taskRepository.findAll();
}
```

At this line:

```java
return taskRepository.findAll();
```

press:

```text
F8
```

This steps over the repository call.

Do not step into Spring Data JPA internals unless you specifically need framework-level debugging.

Then resume:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Option + R` | `F9` |

---

## 10. Debug Flow: GET `/tasks/{id}`

Request:

```bash
curl -i http://localhost:8080/tasks/1
```

Expected backend flow:

```text
TaskController.getTaskById()
→ TaskService.getTaskById()
→ TaskRepository.findById()
→ Database
```

Open `TaskController.java`.

Find:

```java
@GetMapping("/{id}")
public ResponseEntity<Task> getTaskById(@PathVariable Long id) {
    return taskService.getTaskById(id)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
}
```

Set a breakpoint on:

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
taskService
```

Press `F7` to step into:

```java
public Optional<Task> getTaskById(Long id) {
    return taskRepository.findById(id);
}
```

At:

```java
return taskRepository.findById(id);
```

press `F8`.

Then resume.

---

## 11. Debug 404 Flow

Run:

```bash
curl -i http://localhost:8080/tasks/999
```

Expected:

```text
HTTP/1.1 404
```

Set breakpoints in:

```text
TaskController.getTaskById()
TaskService.getTaskById()
```

Inspect:

```text
id = 999
taskRepository.findById(id)
Optional.empty
ResponseEntity.notFound()
```

This helps you understand how a missing database row becomes HTTP `404`.

---

## 12. Debug Flow: POST `/tasks`

Request:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Advanced debugging task","status":"OPEN"}'
```

Expected backend flow:

```text
TaskController.createTask()
→ TaskService.createTask()
→ TaskRepository.save(task)
→ Database
```

Open `TaskController.java`.

Find:

```java
@PostMapping
public ResponseEntity<Task> createTask(@RequestBody Task task) {
    return ResponseEntity.ok(taskService.createTask(task));
}
```

Set a breakpoint on:

```java
return ResponseEntity.ok(taskService.createTask(task));
```

Run the POST curl request.

Inspect:

```text
task
task.id
task.title
task.status
```

Use Evaluate Expression if needed:

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

Press `F7` on:

```java
taskService.createTask(task)
```

You should enter `TaskService.createTask()`:

```java
public Task createTask(Task task) {
    return taskRepository.save(task);
}
```

Set a breakpoint on:

```java
return taskRepository.save(task);
```

Press `F8` to step over the database save.

---

## 13. Easier Debug Version of `createTask()`

For learning, this version is easier to inspect:

```java
public Task createTask(Task task) {
    Task savedTask = taskRepository.save(task);
    return savedTask;
}
```

Set breakpoint on:

```java
return savedTask;
```

Inspect:

```text
savedTask.id
savedTask.title
savedTask.status
```

This clearly shows the task after the database save.

If your ID is generated by the database, it may be `null` before save and populated after save.

---

## 14. Check Database After POST

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

## 15. Debug Flow: PUT `/tasks/{id}`

Request:

```bash
curl -i -X PUT http://localhost:8080/tasks/1 \
  -H "Content-Type: application/json" \
  -d '{"title":"Updated during debugging","status":"COMPLETED"}'
```

Expected backend flow:

```text
TaskController.updateTask()
→ TaskService.updateTask()
→ TaskRepository.findById(id)
→ TaskRepository.save(existingTask)
→ Database
```

Open `TaskController.java`.

Find:

```java
@PutMapping("/{id}")
public ResponseEntity<Task> updateTask(@PathVariable Long id, @RequestBody Task task) {
    return taskService.updateTask(id, task)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
}
```

Set a breakpoint on:

```java
return taskService.updateTask(id, task)
```

Run the PUT curl request.

Inspect:

```text
id
task.title
task.status
```

Step into `TaskService.updateTask()`.

You should reach:

```java
public Optional<Task> updateTask(Long id, Task updatedTask) {
    return taskRepository.findById(id)
            .map(existingTask -> {
                existingTask.setTitle(updatedTask.getTitle());
                existingTask.setStatus(updatedTask.getStatus());
                return taskRepository.save(existingTask);
            });
}
```

Set breakpoints on:

```java
return taskRepository.findById(id)
```

and:

```java
return taskRepository.save(existingTask);
```

Inspect:

```text
id
updatedTask.title
updatedTask.status
existingTask.title before update
existingTask.status before update
existingTask.title after update
existingTask.status after update
```

---

## 16. Debug Flow: DELETE `/tasks/{id}`

Request:

```bash
curl -i -X DELETE http://localhost:8080/tasks/1
```

Expected backend flow:

```text
TaskController.deleteTask()
→ TaskService.deleteTask()
→ TaskRepository.existsById(id)
→ TaskRepository.deleteById(id)
→ Database
```

Open `TaskController.java`.

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

Set a breakpoint on:

```java
if (taskService.deleteTask(id)) {
```

Run:

```bash
curl -i -X DELETE http://localhost:8080/tasks/1
```

Step into `TaskService.deleteTask()`:

```java
public boolean deleteTask(Long id) {
    if (!taskRepository.existsById(id)) {
        return false;
    }

    taskRepository.deleteById(id);
    return true;
}
```

Set breakpoints on:

```java
if (!taskRepository.existsById(id)) {
```

and:

```java
taskRepository.deleteById(id);
```

Inspect:

```text
id
existsById result
deleteById call
return true / false
```

Run the same delete again:

```bash
curl -i -X DELETE http://localhost:8080/tasks/1
```

Expected second result:

```text
HTTP/1.1 404
```

because the row was already deleted.

---

## 17. Conditional Breakpoints

A conditional breakpoint stops only when a condition is true.

Example:

In `TaskController.getTaskById()`, set a breakpoint on:

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

Useful conditions:

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
"COMPLETED".equals(task.getStatus())
```

---

## 18. Logpoints

A logpoint prints a message without stopping the app.

Use logpoints when:

```text
You want to observe execution
You do not want to pause the request
You want temporary debug logging without changing code
```

Open:

```text
TaskService.java
```

Find:

```java
public Task createTask(Task task) {
    return taskRepository.save(task);
}
```

Set a breakpoint on:

```java
return taskRepository.save(task);
```

Right-click the breakpoint.

Change:

```text
Uncheck Suspend
Enable Log message to console
```

Example log message:

```text
createTask called — saving task to database
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
The task is still saved to the database.
```

---

## 19. Exception Breakpoints

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

## 20. Practice Exception Debugging

Create a temporary controller only for practice:

```text
src/main/java/com/example/springbootpractice/controller/DebugErrorController.java
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

Expected:

```text
Debugger stops on the NullPointerException.
```

After practice:

```text
Delete DebugErrorController
or keep it only in a learning branch
```

Do not leave debug-only code in a normal commit.

---

## 21. Read Stack Trace Correctly

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

## 22. Evaluate Expression

When debugger is stopped, use:

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
task.getId()
```

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

## 23. Watches

Watches keep important values visible while stepping.

Add watches such as:

```java
task.getId()
```

```java
task.getTitle()
```

```java
task.getStatus()
```

```java
taskRepository.count()
```

For update debugging, add:

```java
updatedTask.getTitle()
```

```java
updatedTask.getStatus()
```

For delete debugging, add:

```java
id
```

---

## 24. Frames and Call Stack

The Frames panel shows how execution reached the current line.

Example POST flow:

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

Use Frames to understand request path.

---

## 25. Threads View

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

---

## 26. Run to Cursor

If you want to skip several lines and stop at a specific line:

1. Put your cursor on the target line.
2. Use Run to Cursor.

| Mac | Windows/Linux |
|---|---|
| `Option + F9` | `Alt + F9` |

This is faster than pressing `F8` many times.

---

## 27. Show Execution Point

Sometimes you click around and lose the current paused line.

Use:

| Mac | Windows/Linux |
|---|---|
| `Option + F10` | `Alt + F10` |

This jumps back to the current execution line.

---

## 28. Database Debugging Checklist

For database debugging, always confirm these:

```text
App is running in Debug mode
Database is running
application.properties points to the correct database
TaskRepository extends JpaRepository<Task, Long>
TaskService uses taskRepository methods
Repository save/find/delete calls are reached
Database table contains expected rows
```

For H2, check:

```text
http://localhost:8080/h2-console
```

For PostgreSQL Docker, check:

```bash
docker ps
docker logs task-postgres
docker exec -it task-postgres psql -U taskuser -d taskdb
```

SQL:

```sql
SELECT * FROM task;
```

---

## 29. What To Do When You Cannot Find a Method

Use this order.

### Step 1 — Search Everywhere

```text
Shift Shift
```

Search:

```text
TaskController
TaskService
TaskRepository
```

### Step 2 — File Structure

Inside a Java file:

| Mac | Windows/Linux |
|---|---|
| `Cmd + F12` | `Ctrl + F12` |

Search method names:

```text
getAllTasks
getTaskById
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
taskRepository.save
taskRepository.findAll
taskRepository.findById
taskRepository.existsById
taskRepository.deleteById
@GetMapping
@PostMapping
@PutMapping
@DeleteMapping
@RequestMapping("/tasks")
```

---

## 30. Community Edition Replacement Table

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

## 31. Common Debugging Issues

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
TaskService.createTask() means createTask method inside TaskService.java.
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

Search:

```text
taskRepository.save
```

or:

```text
save(task)
```

Make sure `TaskService` has:

```java
private final TaskRepository taskRepository;
```

and:

```java
public Task createTask(Task task) {
    return taskRepository.save(task);
}
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

## 32. Final Debugging Practice

Complete this full flow:

```text
1. Start app in Debug mode.
2. Open TaskController.
3. Find getAllTasks.
4. Set breakpoint on return taskService.getAllTasks().
5. Run curl http://localhost:8080/tasks.
6. Confirm debugger stops.
7. Press F7 to step into TaskService.getAllTasks.
8. Press F8 over taskRepository.findAll().
9. Resume.
10. Find createTask in TaskController.
11. Set breakpoint on taskService.createTask(task).
12. Run POST curl request.
13. Inspect task.title and task.status.
14. Step into TaskService.createTask.
15. Step over taskRepository.save(task).
16. Inspect saved task.
17. Check database table.
18. Debug GET /tasks/1.
19. Debug GET /tasks/999.
20. Debug PUT /tasks/1.
21. Debug DELETE /tasks/1.
22. Add conditional breakpoint id == 999.
23. Add logpoint in createTask.
24. Add NullPointerException exception breakpoint.
25. Practice Evaluate Expression.
26. Add Watches.
27. Remove debug-only code.
```

---

## Module 19 Assignment

Complete these tasks:

```text
1. Open springboot-practice.
2. Confirm TaskRepository extends JpaRepository<Task, Long>.
3. Confirm TaskService uses taskRepository.findAll().
4. Confirm TaskService uses taskRepository.findById(id).
5. Confirm TaskService uses taskRepository.save(task).
6. Confirm TaskService uses taskRepository.existsById(id).
7. Confirm TaskService uses taskRepository.deleteById(id).
8. Start SpringbootPracticeApplication in Debug mode.
9. Open TaskController.
10. Find GET /tasks method.
11. Set breakpoint on taskService.getAllTasks().
12. Run curl http://localhost:8080/tasks.
13. Step into TaskService.getAllTasks().
14. Step over taskRepository.findAll().
15. Resume program.
16. Find POST /tasks method.
17. Set breakpoint on taskService.createTask(task).
18. Run POST /tasks using curl.
19. Inspect task title and status.
20. Step into TaskService.createTask().
21. Step over taskRepository.save(task).
22. Inspect saved task.
23. Check database table.
24. Debug GET /tasks/1.
25. Debug GET /tasks/999.
26. Add conditional breakpoint id == 999.
27. Debug PUT /tasks/1.
28. Debug DELETE /tasks/1.
29. Add logpoint on taskRepository.save(task).
30. Add NullPointerException exception breakpoint.
31. Practice Evaluate Expression.
32. Add Watches.
33. Review console logs.
34. Review Git diff.
35. Remove DebugErrorController if you created it.
36. Commit with message:
    Practice advanced database debugging workflow in IntelliJ Community Edition
```

When done, reply:

```text
Module 19 completed
```
