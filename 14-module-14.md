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
