# Module 16 — Database Integration

## Goal
Connect Spring Boot Task API to a database and use IntelliJ database tools.

You will practice adding JPA/H2 dependencies, configuring H2, converting `Task` to entity, creating repository, replacing in-memory service, adding sample data, using H2 console, using Database tool window, and running SQL.

## Dependencies

Add to `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

For Spring Boot 4.x H2 browser console, you may also need:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-h2console</artifactId>
</dependency>
```

Reload Maven. If dependency transfer failure is cached:

```bash
mvn -U clean package
```

`-U` forces Maven to retry downloads.

## application.properties

```properties
spring.application.name=springboot-practice

spring.datasource.url=jdbc:h2:mem:taskdb
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

spring.h2.console.enabled=true
spring.h2.console.path=/h2-console

server.port=8080
```

## Task.java as JPA Entity

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

## TaskRepository.java

```java
package com.example.springbootpractice.repository;

import com.example.springbootpractice.model.Task;
import org.springframework.data.jpa.repository.JpaRepository;

public interface TaskRepository extends JpaRepository<Task, Long> {
}
```

## TaskService.java Repository Version

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
        if (task.getStatus() == null || task.getStatus().isBlank()) {
            task.setStatus(DEFAULT_STATUS);
        }
        return taskRepository.save(task);
    }

    public Optional<Task> updateTask(Long id, Task updatedTask) {
        return taskRepository.findById(id).map(existingTask -> {
            existingTask.setTitle(updatedTask.getTitle());
            existingTask.setStatus(updatedTask.getStatus() == null || updatedTask.getStatus().isBlank()
                    ? DEFAULT_STATUS
                    : updatedTask.getStatus());
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
            taskRepository.save(new Task("Learn IntelliJ database workflow", "OPEN"));
            taskRepository.save(new Task("Connect Spring Boot with H2 database", "IN_PROGRESS"));
        }
    }
}
```

## H2 Console

Open:

```text
http://localhost:8080/h2-console
```

Login:

```text
JDBC URL: jdbc:h2:mem:taskdb
User Name: sa
Password: empty
```

If you get Whitelabel Error Page:

```text
1. Check spring.h2.console.enabled=true
2. Check /h2-console path
3. Add spring-boot-h2console for Spring Boot 4.x
4. Reload Maven with -U
5. Restart app
```

Your log proving DB works looks like:

```text
Database JDBC URL [jdbc:h2:mem:taskdb]
Hibernate: create table task
Hibernate: insert into task
```

## IntelliJ Database Tool Window

Open:

```text
View → Tool Windows → Database
+ → Data Source → H2
```

Use:

```text
JDBC URL: jdbc:h2:mem:taskdb
User: sa
Password: empty
```

Run SQL:

```sql
SELECT * FROM task;
```

## Assignment

```text
1. Add JPA and H2 dependencies
2. Reload Maven
3. Configure application.properties
4. Convert Task to JPA entity
5. Create TaskRepository
6. Replace TaskService
7. Create DataInitializer
8. Run app
9. Confirm Hibernate creates task table
10. Test GET /tasks
11. Open H2 console
12. Login with jdbc:h2:mem:taskdb
13. Run SELECT * FROM task
14. Open IntelliJ Database tool window
15. Try connecting to H2
16. Run SQL query
17. Test POST and confirm DB changes
```

When done, reply:

```text
Module 16 completed
```
