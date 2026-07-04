# Module 17 — Runtime Management in IntelliJ IDEA Community Edition

## Goal

In this module, you will learn how to manage a running Spring Boot application using **IntelliJ IDEA Community Edition**.

Because you are using **Community Edition**, we will **not depend on IntelliJ Ultimate-only Services features** such as Spring Boot Dashboard, Docker Services, or advanced Spring runtime views.

Instead, we will use:

```text
Run tool window
Debug tool window
Run configurations
IntelliJ Terminal
Browser
curl
Application logs
Port checking commands
Standard Java debugger
```

This workflow is reliable and practical for real development.

---

## 1. What Runtime Management Means

Runtime management means controlling and observing your application while it is running.

You need to know how to:

```text
Start the app
Stop the app
Restart the app
Run on a different port
Read logs
Check if the app is running
Test endpoints
Debug requests
Find port conflicts
Kill stuck processes
Use different run configurations
```

In IntelliJ IDEA Community Edition, you can do all of this without Ultimate tools.

---

## 2. Use Your Spring Boot Project

Open your project:

```text
springboot-practice
```

Main class:

```text
SpringbootPracticeApplication
```

Path should be similar to:

```text
src/main/java/com/example/springbootpractice/SpringbootPracticeApplication.java
```

The class should look similar to:

```java
package com.example.springbootpractice;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringbootPracticeApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootPracticeApplication.class, args);
    }
}
```

In Community Edition, Spring Boot is run as a normal Java application.

---

## 3. Run the Spring Boot App

Open:

```text
SpringbootPracticeApplication.java
```

Click the green Run icon near the `main` method.

Or use shortcut:

| Action | Mac | Windows/Linux |
|---|---|---|
| Run | `Ctrl + R` | `Shift + F10` |

Expected logs:

```text
Tomcat started on port 8080
Started SpringbootPracticeApplication
```

If you see this, your application is running.

---

## 4. Understand the Run Tool Window

After running the app, IntelliJ opens the **Run** tool window.

You should see:

```text
Console logs
Rerun button
Stop button
Scroll to end
Soft wrap option
Clear console
Application output
Spring Boot startup logs
Hibernate SQL logs if enabled
```

Important buttons:

| Button | Meaning |
|---|---|
| Green circular arrow | Rerun |
| Red square | Stop |
| Trash/clear icon | Clear console |
| Pin icon | Keep tab |
| Scroll icon | Scroll to end |

---

## 5. Stop the App

Use the red Stop button in the Run window.

Shortcut:

| Action | Mac | Windows/Linux |
|---|---|---|
| Stop | `Cmd + F2` | `Ctrl + F2` |

After stopping, the console may show:

```text
Process finished with exit code 130
```

or similar. That is normal.

---

## 6. Rerun the App

Use the Rerun button in the Run window.

Or stop and run again using:

| Action | Mac | Windows/Linux |
|---|---|---|
| Run | `Ctrl + R` | `Shift + F10` |

This is useful after code or configuration changes.

---

## 7. Test the Running App

Open browser:

```text
http://localhost:8080/tasks
```

Or use IntelliJ Terminal:

```bash
curl http://localhost:8080/tasks
```

Expected: JSON response.

Example:

```json
[
  {
    "id": 1,
    "title": "Learn H2 database in Community Edition",
    "status": "OPEN"
  }
]
```

The exact response depends on your current project data.

---

## 8. Open IntelliJ Terminal

Use:

```text
View → Tool Windows → Terminal
```

Shortcut:

| Mac | Windows/Linux |
|---|---|
| `Option + F12` | `Alt + F12` |

The Terminal is important in Community Edition because it replaces many Ultimate-only runtime tools.

You will use Terminal for:

```text
curl requests
Maven commands
Docker commands
Port checks
Process checks
Git commands if needed
```

---

## 9. Create a Run Configuration

Go to:

```text
Run → Edit Configurations
```

Click:

```text
+
```

Choose:

```text
Application
```

Set:

```text
Name: Spring Boot Local 8080
Main class: com.example.springbootpractice.SpringbootPracticeApplication
Use classpath of module: springboot-practice
JRE: Java 21
```

Apply and save.

Now you can run the app from the top-right configuration selector.

---

## 10. Create a Second Run Configuration for Port 8081

Go to:

```text
Run → Edit Configurations
```

Duplicate your existing configuration or create a new one.

Set:

```text
Name: Spring Boot Local 8081
Main class: com.example.springbootpractice.SpringbootPracticeApplication
Program arguments: --server.port=8081
```

Apply and save.

Run this configuration.

Expected log:

```text
Tomcat started on port 8081
```

Test:

```bash
curl http://localhost:8081/tasks
```

Important: Do not run both 8080 and 8081 configurations at the same time unless your database setup supports multiple app instances.

---

## 11. Alternative: Set Port in `application.properties`

You can also change the port in:

```text
src/main/resources/application.properties
```

Example:

```properties
server.port=8081
```

But for learning runtime management, using run configuration arguments is better because you can switch ports without editing the file.

Priority note:

```text
Program argument --server.port=8081 overrides server.port=8080 in application.properties.
```

---

## 12. Read Application Logs

When the app starts, check for important log lines.

### Good Startup Logs

```text
Tomcat started on port 8080
Started SpringbootPracticeApplication
```

### Database Logs

For H2:

```text
jdbc:h2:mem:taskdb
```

For PostgreSQL:

```text
jdbc:postgresql://localhost:5432/taskdb
```

### Hibernate SQL Logs

If you enabled:

```properties
spring.jpa.show-sql=true
```

You may see:

```text
Hibernate: select ...
Hibernate: insert ...
Hibernate: update ...
```

These logs help confirm database activity.

---

## 13. Search in Console Output

If your console has many lines, use search.

Click inside Run console and use:

| Action | Mac | Windows/Linux |
|---|---|---|
| Find | `Cmd + F` | `Ctrl + F` |

Search for:

```text
Tomcat started
Started
ERROR
WARN
jdbc
Hibernate
Exception
Caused by
```

This helps you quickly understand startup problems.

---

## 14. Common Runtime Problem: Port 8080 Already in Use

Sometimes you may see:

```text
Web server failed to start. Port 8080 was already in use.
```

This means another app is already using port `8080`.

### Check Port on Mac/Linux

```bash
lsof -i :8080
```

Example output:

```text
COMMAND   PID       USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
java     12345      user   84u  IPv6  ...         TCP *:http-alt (LISTEN)
```

Kill process:

```bash
kill -9 12345
```

Replace `12345` with the actual PID.

### Check Port on Windows

```bash
netstat -ano | findstr :8080
```

Then kill:

```bash
taskkill /PID <PID> /F
```

---

## 15. Run App from Terminal Using Maven

Sometimes you may want to run Spring Boot outside the IntelliJ Run button.

Use:

```bash
mvn spring-boot:run
```

If your app needs a different port:

```bash
mvn spring-boot:run -Dspring-boot.run.arguments=--server.port=8081
```

Stop it with:

```text
Ctrl + C
```

This is useful when checking whether an issue is IntelliJ-specific or project-specific.

---

## 16. Package and Run the JAR

Build the project:

```bash
mvn clean package
```

Run the generated JAR:

```bash
java -jar target/*.jar
```

If you want another port:

```bash
java -jar target/*.jar --server.port=8081
```

This teaches you how the app runs outside IntelliJ.

---

## 17. Debug the App

Open:

```text
TaskController.java
```

Set a breakpoint in:

```text
getAllTasks
createTask
updateTask
deleteTask
```

Start the app in Debug mode.

Shortcut:

| Action | Mac | Windows/Linux |
|---|---|---|
| Debug | `Ctrl + D` | `Shift + F9` |

Call:

```bash
curl http://localhost:8080/tasks
```

The debugger should stop at your breakpoint.

---

## 18. Debug Request Flow

For GET request:

```text
curl http://localhost:8080/tasks
```

Trace:

```text
TaskController.getAllTasks
→ TaskService.getAllTasks
→ TaskRepository.findAll
→ Database
```

Use debugger buttons:

| Action | Mac | Windows/Linux |
|---|---|---|
| Step Over | `F8` | `F8` |
| Step Into | `F7` | `F7` |
| Step Out | `Shift + F8` | `Shift + F8` |
| Resume | `Cmd + Option + R` | `F9` |
| Evaluate Expression | `Option + F8` | `Alt + F8` |

---

## 19. Debug POST Request

Set breakpoint in:

```text
TaskController.createTask
TaskService.createTask
```

Run this request:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Runtime debug test","status":"OPEN"}'
```

Inspect variables:

```text
request body
task title
task status
saved task id
response object
```

This is one of the most important debugging workflows.

---

## 20. Use Environment Variables in Run Configuration

Open:

```text
Run → Edit Configurations
```

Select your app configuration.

Find:

```text
Environment variables
```

Add:

```text
APP_MODE=local
```

Create a test endpoint or print it temporarily:

```java
String appMode = System.getenv("APP_MODE");
System.out.println("APP_MODE = " + appMode);
```

Run the app.

Expected console:

```text
APP_MODE = local
```

Do not print real secrets in production code.

---

## 21. Use Program Arguments

In Run Configuration:

```text
Program arguments
```

Set:

```text
--server.port=8081
```

Run the app.

Expected:

```text
Tomcat started on port 8081
```

This is useful for local testing.

---

## 22. Use VM Options

In Run Configuration, you may see:

```text
VM options
```

Example:

```text
-Dapp.mode=local
```

Read it in Java:

```java
String mode = System.getProperty("app.mode");
System.out.println("app.mode = " + mode);
```

Difference:

| Type | Example | Read With |
|---|---|---|
| Program argument | `--server.port=8081` | Spring Boot properties |
| Environment variable | `APP_MODE=local` | `System.getenv("APP_MODE")` |
| VM option | `-Dapp.mode=local` | `System.getProperty("app.mode")` |

---

## 23. Runtime Health Check

Add a simple health controller if you do not already have Actuator.

Create:

```text
controller/HealthController.java
```

```java
package com.example.springbootpractice.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HealthController {

    @GetMapping("/health")
    public String health() {
        return "OK";
    }
}
```

Run app.

Test:

```bash
curl http://localhost:8080/health
```

Expected:

```text
OK
```

This helps you quickly confirm the app is alive.

---

## 24. Optional: Add Spring Boot Actuator

If you want a more realistic health endpoint, add dependency:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Reload Maven.

Add to `application.properties`:

```properties
management.endpoints.web.exposure.include=health,info
```

Run:

```bash
curl http://localhost:8080/actuator/health
```

Expected:

```json
{"status":"UP"}
```

This is optional for Module 17.

---

## 25. Community Edition Runtime Workflow

Use this workflow when developing:

```text
1. Start app using Run configuration
2. Watch Run console logs
3. Test endpoint with curl/browser
4. Debug if response is wrong
5. Check port if app fails to start
6. Stop app before changing database/runtime config
7. Restart app after property changes
8. Review logs for ERROR, WARN, jdbc, Hibernate
```

This replaces the need for Ultimate runtime dashboards.

---

## 26. Troubleshooting

### Issue 1 — App Does Not Start

Check console for:

```text
ERROR
Caused by
Port already in use
BeanCreationException
Database connection failed
```

### Issue 2 — Endpoint Returns 404

Check:

```text
Controller has @RestController
Method has @GetMapping/@PostMapping
Path is correct
App restarted after change
Request URL is correct
```

Search in code:

```text
/tasks
@GetMapping
@PostMapping
@RequestMapping
```

### Issue 3 — curl Cannot Connect

Error:

```text
Connection refused
```

Meaning:

```text
App is not running, wrong port, or startup failed.
```

Check:

```bash
curl http://localhost:8080/health
```

Check logs.

### Issue 4 — App Still Uses Old Config

Stop app fully.

Start again.

Check `application.properties` is saved.

Check run configuration does not override the value.

### Issue 5 — Debugger Does Not Stop

Check:

```text
App is running in Debug mode, not Run mode
Breakpoint is in executed code path
Request URL triggers that method
Breakpoint is enabled
Code was recompiled/restarted after major changes
```

---

## 27. Community Edition Important Note

In IntelliJ IDEA Ultimate, you may see a Services tool window with Spring Boot runtime grouping.

In Community Edition, use:

| Need | Community Edition Method |
|---|---|
| Start app | Run main class |
| Stop app | Run window Stop button |
| Restart app | Rerun button |
| Logs | Run console |
| Test endpoint | Browser/curl/Postman |
| Check port | `lsof`, `netstat` |
| Debug request | Java debugger |
| Run different port | Program argument `--server.port=8081` |
| Run outside IDE | `mvn spring-boot:run` or `java -jar` |

This is enough for real Spring Boot development.

---

## 28. Final Check

Before completing this module, confirm:

```text
You can run Spring Boot from main class
You can stop and rerun the app
You can create/edit run configurations
You can run app on port 8081
You can test GET /tasks with curl
You can debug GET /tasks
You can debug POST /tasks
You can identify and fix port conflicts
You can run the app from Terminal using Maven
You can read logs and search for important messages
```

---

## Module 17 Assignment

Complete these tasks:

```text
1. Open springboot-practice
2. Run SpringbootPracticeApplication
3. Confirm Tomcat starts on port 8080
4. Test GET /tasks using browser or curl
5. Stop the app
6. Rerun the app
7. Open Run → Edit Configurations
8. Create configuration: Spring Boot Local 8080
9. Create configuration: Spring Boot Local 8081
10. Add program argument --server.port=8081 to the 8081 config
11. Run the 8081 configuration
12. Test GET /tasks on port 8081
13. Set a breakpoint in TaskController.getAllTasks
14. Debug the app
15. Call GET /tasks with curl
16. Step from controller to service
17. Set breakpoint in TaskController.createTask
18. Debug POST /tasks with curl
19. Use Terminal to run lsof -i :8080 or equivalent
20. Run the app using mvn spring-boot:run
21. Stop terminal run using Ctrl + C
22. Optional: add /health endpoint
23. Review Git diff
24. Commit with message:
    Add runtime management practice notes
```

When done, reply:

```text
Module 17 completed
```
