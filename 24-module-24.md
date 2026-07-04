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
