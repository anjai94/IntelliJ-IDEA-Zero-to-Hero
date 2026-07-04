# Module 17 — Services Tool Window and Runtime Management

## Goal
Use IntelliJ Services tool window to manage running applications, databases, Docker containers, and multiple run configurations.

## Open Services

```text
View → Tool Windows → Services
```

Shortcut is keymap dependent, often:

```text
Alt + 8
```

## Add Spring Boot Run Configuration

Run your Spring Boot app once. It should appear in Services.

If not:

```text
Services → + → Run Configuration Type → Application/Spring Boot
```

## Practice Controls

From Services, practice:

```text
Run
Stop
Rerun
Debug
Open console
Clear console
Scroll logs
```

## Multiple Configurations

Create two run configs:

```text
Spring Boot Practice - 8080
Program args: --server.port=8080
```

```text
Spring Boot Practice - 8081
Program args: --server.port=8081
```

Test:

```text
http://localhost:8080/tasks
http://localhost:8081/tasks
```

## Debug from Services

Add breakpoint:

```text
TaskController.getAllTasks
TaskService.getAllTasks
```

Click Debug in Services and run:

```http
GET http://localhost:8080/tasks
```

## Logs

Review:

```text
Startup logs
Tomcat port
Hibernate SQL
Errors
Stack traces
Request logs
```

## Services Can Show

```text
Spring Boot apps
Docker containers
Docker Compose services
Database connections
Application run configs
Gradle/Maven tasks
```

## Assignment

```text
1. Open Services
2. Run Spring Boot app from Services
3. Stop app
4. Rerun app
5. Debug app
6. Add breakpoint in TaskController
7. Run HTTP request and hit breakpoint
8. Create 8080 config
9. Create 8081 config
10. Run both if possible
11. Review logs
12. Stop all running apps
```

When done, reply:

```text
Module 17 completed
```
