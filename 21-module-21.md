# Module 21 — Security-Focused IntelliJ Usage

## Goal
Use IntelliJ IDEA for practical security-focused development and review.

You will practice finding hardcoded secrets, inspections, Structural Search, unsafe logging, vulnerable dependencies, basic validation, global error handling, security review notes, `.gitignore`, Inspect Code, and Git diff review.

## Use Project

```text
springboot-practice
```

## Practice 1 — Hardcoded Secret Detection

Create package:

```text
com.example.springbootpractice.securityreview
```

Create `SecretDemo`:

```java
package com.example.springbootpractice.securityreview;

public class SecretDemo {

    private static final String DB_PASSWORD = "admin123";
    private static final String API_TOKEN = "abc123-secret-token";

    public void connect() {
        System.out.println("Connecting with password: " + DB_PASSWORD);
        System.out.println("Using token: " + API_TOKEN);
    }
}
```

This is intentionally unsafe.

Open:

```text
Settings → Editor → Inspections
```

Search:

```text
Hardcoded
Password
```

## Replace with Safer Version

```java
package com.example.springbootpractice.securityreview;

public class SecretDemo {

    private static final String DB_PASSWORD_ENV = "DB_PASSWORD";
    private static final String API_TOKEN_ENV = "API_TOKEN";

    public void connect() {
        String dbPassword = System.getenv(DB_PASSWORD_ENV);
        String apiToken = System.getenv(API_TOKEN_ENV);

        if (dbPassword == null || apiToken == null) {
            throw new IllegalStateException("Required environment variables are missing");
        }

        System.out.println("Connecting with environment-based credentials");
    }
}
```

Rules:

```text
Do not print secrets
Do not commit real passwords
Use environment variables or secret manager
```

## Practice 2 — Unsafe Logging

Create `UnsafeLoggingDemo`:

```java
package com.example.springbootpractice.securityreview;

public class UnsafeLoggingDemo {

    public void login(String username, String password) {
        System.out.println("Login attempt for " + username + " with password " + password);
    }
}
```

Search:

```text
System.out.println
password
token
secret
```

Fix:

```java
package com.example.springbootpractice.securityreview;

public class UnsafeLoggingDemo {

    public void login(String username, String password) {
        System.out.println("Login attempt for user: " + username);
    }
}
```

## Practice 3 — Structural Search

Use:

```text
Find Action → Search Structurally
```

Search:

```java
System.out.println($TEXT$);
```

## Practice 4 — Vulnerable Dependencies

Open:

```text
View → Tool Windows → Vulnerable Dependencies
```

Temporarily add old dependency:

```xml
<dependency>
    <groupId>commons-collections</groupId>
    <artifactId>commons-collections</artifactId>
    <version>3.2.1</version>
</dependency>
```

Reload Maven, review warning, then remove dependency.

## Practice 5 — Add Basic Validation

In `TaskService.createTask`:

```java
public Task createTask(Task task) {
    if (task.getTitle() == null || task.getTitle().isBlank()) {
        throw new IllegalArgumentException("Task title is required");
    }

    if (task.getStatus() == null || task.getStatus().isBlank()) {
        task.setStatus("OPEN");
    }

    return taskRepository.save(task);
}
```

## Practice 6 — Global Exception Handler

Create:

```text
com.example.springbootpractice.exception.GlobalExceptionHandler
```

```java
package com.example.springbootpractice.exception;

import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(IllegalArgumentException.class)
    public ResponseEntity<String> handleIllegalArgumentException(IllegalArgumentException exception) {
        return ResponseEntity.badRequest().body(exception.getMessage());
    }
}
```

## Invalid HTTP Request

```http
### Create invalid task - blank title
POST {{baseUrl}}/tasks
Content-Type: application/json

{
  "title": "",
  "status": "OPEN"
}
```

Expected:

```text
HTTP 400
Task title is required
```

## security-review-notes.md

Create:

```text
src/test/security-review-notes.md
```

```markdown
# Security Review Notes

## Checked Areas
- Hardcoded secrets
- Unsafe logging
- Input validation
- Error handling
- Vulnerable dependencies
- Private env files
- Git diff before commit

## Findings
- Avoid logging passwords/tokens.
- Avoid hardcoded secrets.
- Validate task title.
- Do not commit private HTTP Client env files.
- Remove intentionally vulnerable dependencies after testing.

## Future Improvements
- Add authentication.
- Add authorization.
- Add DTO validation annotations.
- Add structured error response.
- Add dependency scanning in CI.
```

## .gitignore

```gitignore
.env
*.env.local
http-client.private.env.json
**/http-client.private.env.json
```

## Inspect Code

```text
Analyze → Inspect Code
```

Do not automatically fix everything; understand each warning.

## Assignment

```text
1. Create securityreview package
2. Create SecretDemo with hardcoded values
3. Review IntelliJ inspections
4. Replace with environment-based version
5. Create UnsafeLoggingDemo
6. Search System.out.println/password/token/secret
7. Fix unsafe logging
8. Use Structural Search
9. Open Vulnerable Dependencies
10. Temporarily add old commons-collections dependency
11. Reload Maven and review warning
12. Remove old dependency
13. Add validation in TaskService
14. Create GlobalExceptionHandler
15. Add invalid HTTP request
16. Confirm 400 response
17. Create security-review-notes.md
18. Update .gitignore
19. Run Inspect Code
20. Review Git diff
```

When done, reply:

```text
Module 21 completed
```
