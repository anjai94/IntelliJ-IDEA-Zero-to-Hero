# Module 13 — Spring Boot Project Setup

## Goal
Create and run a Spring Boot project from IntelliJ IDEA.

You will practice Spring project creation, dependency selection, main class, running Spring Boot, creating a controller, editing `application.properties`, changing port, and reading logs.

## Create Project

Create:

```text
springboot-practice
```

Use:

```text
Spring Boot
Maven
Java 21
Group: com.example
Artifact: springboot-practice
Dependency: Spring Web
```

## Main Class

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

Run it. Expected logs:

```text
Tomcat started on port 8080
Started SpringbootPracticeApplication
```

## HelloController.java

Create package:

```text
com.example.springbootpractice.controller
```

Create:

```java
package com.example.springbootpractice.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello from Spring Boot and IntelliJ IDEA";
    }

    @GetMapping("/greet")
    public String greet() {
        return "Welcome to the IntelliJ Spring Boot module";
    }
}
```

Open:

```text
http://localhost:8080/hello
http://localhost:8080/greet
```

## Run Configuration

Rename configuration:

```text
Spring Boot Practice - Local
```

Check:

```text
Main class
Module
JDK
Environment variables
Program arguments
```

## Change Port

In `application.properties`:

```properties
server.port=8081
```

Restart and test:

```text
http://localhost:8081/hello
```

Change back:

```properties
server.port=8080
```

## Common Issues

```text
Port already in use → stop old app or change port
Whitelabel Error Page → URL has no matching endpoint
Controller not found → package must be under root package
```

## Assignment

```text
1. Create springboot-practice
2. Add Spring Web
3. Run main class
4. Create controller package
5. Create HelloController
6. Test /hello
7. Test /greet
8. Rename run configuration
9. Change port to 8081
10. Test again
11. Change port back to 8080
12. Review logs
```

When done, reply:

```text
Module 13 completed
```
