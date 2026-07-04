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
