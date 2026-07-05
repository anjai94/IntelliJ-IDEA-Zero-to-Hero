# Module 20 — IntelliJ Productivity Mastery in Community Edition

## Goal

In this module, you will learn how to move around your Spring Boot project faster using **IntelliJ IDEA Community Edition**.

This module is not about adding new business logic. It is about learning how to find files, find methods, jump between controller/service/repository, search code, and avoid wasting time clicking folders.

You will practice using:

```text
Search Everywhere
Find in Files
File Structure
Go to Declaration
Find Usages
Recent Files
Terminal
Git Diff
TODO search
Local History
```

---

## 1. First Confirm Your Project Structure

Your project should be similar to this:

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

If your project is not exactly the same, that is okay. But you should at least have:

```text
TaskController
TaskService
TaskRepository
Task
application.properties
pom.xml
```

---

## 2. How to Find `TaskController`

Do not manually click folders first.

Use **Search Everywhere**.

Press:

```text
Shift Shift
```

Then type:

```text
TaskController
```

Open:

```text
TaskController.java
```

If you cannot find `TaskController`, then your controller may not exist yet.

In that case, create this package:

```text
src/main/java/com/example/springbootpractice/controller
```

Then create this class:

```text
TaskController.java
```

---

## 3. What `TaskController` Should Look Like

Your `TaskController` should look similar to this:

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

Important: at your current stage, you may not have `TaskResponse` or `TaskMapper`. That is fine. Use the simple `Task` version above.

---

## 4. How to Find `getAllTasks()`

Open `TaskController.java`.

Then use **File Structure**.

Press:

| Mac | Windows/Linux |
|---|---|
| `Cmd + F12` | `Ctrl + F12` |

A small popup will show all methods in the file.

Look for:

```text
getAllTasks
```

Select it and press Enter.

You should land here:

```java
@GetMapping
public List<Task> getAllTasks() {
    return taskService.getAllTasks();
}
```

This is the method for:

```bash
curl http://localhost:8080/tasks
```

---

## 5. How to Find `createTask()`

Stay inside `TaskController.java`.

Again press:

| Mac | Windows/Linux |
|---|---|
| `Cmd + F12` | `Ctrl + F12` |

Search inside the popup:

```text
createTask
```

Open it.

You should find:

```java
@PostMapping
public ResponseEntity<Task> createTask(@RequestBody Task task) {
    return ResponseEntity.ok(taskService.createTask(task));
}
```

This is the method for:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Test task","status":"OPEN"}'
```

---

## 6. How to Jump from Controller to Service

In `TaskController`, find this line:

```java
return taskService.getAllTasks();
```

Put your mouse on:

```text
getAllTasks
```

Then use:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Click` | `Ctrl + Click` |

IntelliJ should jump to `TaskService.getAllTasks()`.

You should land here:

```java
public List<Task> getAllTasks() {
    return taskRepository.findAll();
}
```

This is how you follow the code flow:

```text
TaskController
→ TaskService
→ TaskRepository
```

---

## 7. How to Go Back to Previous File

After jumping to `TaskService`, go back to `TaskController`.

Use:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Option + Left` | `Ctrl + Alt + Left` |

This is very useful.

Example workflow:

```text
TaskController → Cmd/Ctrl Click → TaskService
TaskService → Navigate Back → TaskController
```

---

## 8. How to Find `TaskService`

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

Your service should look similar to this:

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

## 9. How to Find `createTask()` in `TaskService`

Open `TaskService.java`.

Press:

| Mac | Windows/Linux |
|---|---|
| `Cmd + F12` | `Ctrl + F12` |

Search:

```text
createTask
```

You should find:

```java
public Task createTask(Task task) {
    return taskRepository.save(task);
}
```

This is where the task is saved to the database.

If your method looks like this instead:

```java
public Task createTask(Task task) {
    task.setId(nextId++);
    tasks.add(task);
    return task;
}
```

that means you still have the older in-memory version.

Both are okay for navigation practice, but for database modules you should use:

```java
public Task createTask(Task task) {
    return taskRepository.save(task);
}
```

---

## 10. How to Find `TaskRepository`

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

It should look like this:

```java
package com.example.springbootpractice.repository;

import com.example.springbootpractice.model.Task;
import org.springframework.data.jpa.repository.JpaRepository;

public interface TaskRepository extends JpaRepository<Task, Long> {
}
```

This file may look small, but it gives you methods like:

```text
findAll()
findById()
save()
deleteById()
existsById()
```

Spring Data JPA creates these methods automatically.

---

## 11. Full Request Flow You Must Understand

For this request:

```bash
curl http://localhost:8080/tasks
```

The flow is:

```text
TaskController.getAllTasks()
→ TaskService.getAllTasks()
→ TaskRepository.findAll()
→ Database
```

For this request:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"New task","status":"OPEN"}'
```

The flow is:

```text
TaskController.createTask()
→ TaskService.createTask()
→ TaskRepository.save()
→ Database
```

For this request:

```bash
curl -i http://localhost:8080/tasks/1
```

The flow is:

```text
TaskController.getTaskById()
→ TaskService.getTaskById()
→ TaskRepository.findById()
→ Database
```

For this request:

```bash
curl -i -X PUT http://localhost:8080/tasks/1 \
  -H "Content-Type: application/json" \
  -d '{"title":"Updated task","status":"COMPLETED"}'
```

The flow is:

```text
TaskController.updateTask()
→ TaskService.updateTask()
→ TaskRepository.findById()
→ TaskRepository.save()
→ Database
```

For this request:

```bash
curl -i -X DELETE http://localhost:8080/tasks/1
```

The flow is:

```text
TaskController.deleteTask()
→ TaskService.deleteTask()
→ TaskRepository.existsById()
→ TaskRepository.deleteById()
→ Database
```

---

## 12. Use Find in Files When You Cannot Find a Method

If you cannot find a method manually, use **Find in Files**.

Press:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Shift + F` | `Ctrl + Shift + F` |

Search:

```text
getAllTasks
```

or:

```text
createTask
```

or:

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

This is the fastest way to find methods when you are lost.

---

## 13. Exact Search Terms to Use

Use these searches:

```text
TaskController
```

```text
TaskService
```

```text
TaskRepository
```

```text
getAllTasks
```

```text
createTask
```

```text
updateTask
```

```text
deleteTask
```

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

These searches will help you find almost everything in this project.

---

## 14. Productivity Practice: Find Every REST Method

Open `TaskController.java`.

Use `Cmd + F12` or `Ctrl + F12`.

Find these methods one by one:

```text
getAllTasks
getTaskById
createTask
updateTask
deleteTask
```

For each method, write down the HTTP endpoint:

| Method | HTTP Request |
|---|---|
| `getAllTasks()` | `GET /tasks` |
| `getTaskById(Long id)` | `GET /tasks/{id}` |
| `createTask(Task task)` | `POST /tasks` |
| `updateTask(Long id, Task task)` | `PUT /tasks/{id}` |
| `deleteTask(Long id)` | `DELETE /tasks/{id}` |

---

## 15. Productivity Practice: Jump Controller to Service

In `TaskController`, do this:

1. Find `getAllTasks()`.
2. Cmd/Ctrl-click `taskService.getAllTasks()`.
3. Confirm you moved to `TaskService.getAllTasks()`.
4. Navigate back.
5. Find `createTask()`.
6. Cmd/Ctrl-click `taskService.createTask(task)`.
7. Confirm you moved to `TaskService.createTask()`.
8. Navigate back.

This is the main skill for understanding Spring Boot code.

---

## 16. Productivity Practice: Service to Repository

In `TaskService`, do this:

1. Find `getAllTasks()`.
2. Cmd/Ctrl-click `taskRepository.findAll()`.
3. You may go to Spring Data JPA generated method/library code.
4. Navigate back.
5. Find `createTask()`.
6. Cmd/Ctrl-click `taskRepository.save(task)`.

You do not need to understand all Spring library code. The important point is:

```text
Repository methods talk to the database.
```

---

## 17. Recent Files

Use Recent Files to switch between files quickly.

Press:

| Mac | Windows/Linux |
|---|---|
| `Cmd + E` | `Ctrl + E` |

Practice switching between:

```text
TaskController
TaskService
TaskRepository
Task
application.properties
pom.xml
```

This is faster than clicking tabs.

---

## 18. Search Everywhere

Use Search Everywhere for files/classes.

Press:

```text
Shift Shift
```

Search and open:

```text
TaskController
TaskService
TaskRepository
Task
SpringbootPracticeApplication
application.properties
pom.xml
```

Do this until it feels easy.

---

## 19. Find Action

Use Find Action when you forget where something is.

Press:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Shift + A` | `Ctrl + Shift + A` |

Search actions like:

```text
Reformat Code
Optimize Imports
Reload All Maven Projects
Local History
New Scratch File
Find Usages
Search Structurally
```

---

## 20. Add TODO Comments

Add this in `TaskController.java`:

```java
// TODO: Add authentication before production use
```

Add this in `TaskService.java`:

```java
// TODO: Add validation before saving task
```

Now open TODO window using Find Action:

```text
Find Action → TODO
```

You should see your TODO comments.

---

## 21. Find Usages

Find Usages shows where something is used.

Click on:

```text
createTask
```

Then press:

| Mac | Windows/Linux |
|---|---|
| `Option + F7` | `Alt + F7` |

Try Find Usages on:

```text
TaskService
createTask
getAllTasks
TaskRepository
Task
```

Before changing or deleting a method, always use Find Usages.

---

## 22. Reformat Code

Before committing, reformat your code.

Press:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Option + L` | `Ctrl + Alt + L` |

Use this on:

```text
TaskController.java
TaskService.java
Task.java
```

---

## 23. Optimize Imports

Before committing, optimize imports.

Press:

| Mac | Windows/Linux |
|---|---|
| `Ctrl + Option + O` | `Ctrl + Alt + O` |

This removes unused imports.

---

## 24. Check for Debug Code Before Commit

Use Find in Files:

| Mac | Windows/Linux |
|---|---|
| `Cmd + Shift + F` | `Ctrl + Shift + F` |

Search:

```text
System.out.println
```

```text
debug
```

```text
temporary
```

```text
password
```

```text
secret
```

Remove anything that should not be committed.

---

## 25. Review Git Diff

Open Commit window:

| Mac | Windows/Linux |
|---|---|
| `Cmd + 0` | `Alt + 0` |

Review changed files.

Check for:

```text
Unrelated changes
Temporary debug code
Wrong formatting
Accidental file changes
Secrets/passwords
target/ folder
```

Good productivity means you review before committing.

---

## Module 20 Assignment

Complete these tasks:

```text
1. Open springboot-practice.
2. Press Shift Shift and open TaskController.
3. Use Cmd/Ctrl + F12 to find getAllTasks.
4. Use Cmd/Ctrl + F12 to find createTask.
5. In getAllTasks, Cmd/Ctrl-click taskService.getAllTasks().
6. Confirm IntelliJ opens TaskService.getAllTasks.
7. Navigate back to TaskController.
8. In createTask, Cmd/Ctrl-click taskService.createTask(task).
9. Confirm IntelliJ opens TaskService.createTask.
10. Navigate back to TaskController.
11. Press Shift Shift and open TaskRepository.
12. Confirm it extends JpaRepository<Task, Long>.
13. Press Shift Shift and open Task.java.
14. Confirm it has fields id, title, status.
15. Use Find in Files to search getAllTasks.
16. Use Find in Files to search createTask.
17. Use Find in Files to search @GetMapping.
18. Use Find in Files to search @PostMapping.
19. Use Recent Files to switch between TaskController and TaskService.
20. Add TODO comment in TaskController.
21. Add TODO comment in TaskService.
22. Open TODO window.
23. Use Find Usages on createTask.
24. Reformat TaskController.
25. Optimize imports.
26. Search for System.out.println before commit.
27. Review Git diff.
28. Commit with message:
    Practice IntelliJ navigation and productivity workflow
```

When done, reply:

```text
Module 20 completed
```
