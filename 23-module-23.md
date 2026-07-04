# Module 23 — AI-Assisted Development in IntelliJ IDEA

## Goal
Use AI inside IntelliJ responsibly and safely.

You will practice AI Chat, explaining code, generating tests, refactoring suggestions, commit messages, HTTP Client help, debugging guidance, security review prompts, privacy rules, and AI restrictions.

## Important Rule

AI is an assistant, not the final authority.

Use AI for:

```text
Explaining code
Draft tests
Small refactoring suggestions
Commit messages
Documentation drafts
Change summaries
Possible issue spotting
```

Do not blindly trust AI for:

```text
Security fixes
Authentication
Authorization
Cryptography
Production config
Dependency upgrade decisions
Database migrations
Compliance-sensitive work
```

## Check Availability

```text
Settings → Plugins → AI Assistant
View → Tool Windows → AI Assistant
Shift Shift → AI Assistant
```

## Practice 1 — Explain Code

Open `TaskController.java`, select:

```java
@GetMapping("/{id}")
public ResponseEntity<Task> getTaskById(@PathVariable Long id) {
    return taskService.getTaskById(id)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
}
```

Ask:

```text
Explain this Spring Boot controller method in simple terms.
```

Expected explanation should mention:

```text
@GetMapping
@PathVariable
Optional
ResponseEntity.ok
404
```

## Better Prompting

Bad:

```text
Explain this.
```

Better:

```text
Explain this Spring Boot controller method as if I am learning IntelliJ and Spring Boot. Focus on how request flow moves from controller to service.
```

Best:

```text
Explain this method in 5 bullet points. Then tell me where I should place a breakpoint to debug it in IntelliJ.
```

## Generate Unit Tests

Open `TaskService.java` and ask:

```text
Generate unit tests for TaskService createTask and updateTask. Use JUnit 5 and Mockito. Keep tests simple and readable.
```

Review:

```text
Imports
Framework
Mocks
Assertions
No fake methods/classes
No unnecessary complexity
```

## Review AI Diff

```text
1. Read generated code
2. Check changed files
3. Accept only useful changes
4. Reject incorrect changes
5. Run tests
6. Review Git diff
```

## Refactoring Prompt

```text
Review this service class and suggest small refactoring improvements. Do not change behavior.
```

Then:

```text
Show only the smallest safe refactoring for createTask.
```

## Commit Message Prompt

```text
Generate a concise commit message for the selected changes. Use imperative style.
```

Good:

```text
Add task validation error handling
```

Bad:

```text
Updated files
```

## HTTP Client Prompt

```text
Add HTTP Client requests to test invalid task creation and confirm blank title returns 400.
```

Expected:

```http
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
```

## Debugging Prompt

```text
I am debugging POST /tasks in IntelliJ. Tell me where to place breakpoints and what variables to inspect.
```

Good locations:

```text
TaskController.createTask
TaskService.createTask
TaskRepository.save
GlobalExceptionHandler
```

## Security Review Prompt

```text
Review these files for basic application security concerns. Focus on validation, error handling, logging, and access control gaps. Do not rewrite the code yet.
```

Expected gaps:

```text
No authentication
No authorization
Limited validation
Simple errors
Need DTOs
Need centralized validation
```

## Data Privacy

Do not paste/share:

```text
production passwords
API keys
customer data
private certs
tokens
company confidential code
security incident details
real customer vulnerabilities
```

## AI Review Checklist

```text
1. Code compiles?
2. Imports correct?
3. Method/class names real?
4. Behavior changed unexpectedly?
5. Too complex?
6. Sensitive data exposed?
7. Security weakened?
8. Vulnerable dependency added?
9. Tests passed?
10. Git diff reviewed?
```

## Assignment

```text
1. Confirm AI Assistant availability
2. Explain getTaskById
3. Ask breakpoint locations
4. Ask TaskService refactoring suggestions
5. Generate tests if available
6. Review AI Diff
7. Run tests
8. Generate invalid HTTP request
9. Run invalid request
10. Ask AI for security concerns
11. Generate/compare commit message
12. Review Git diff manually
13. Open AI settings
14. Review privacy options
15. Write 5 safe AI rules in README-practice.md
```

When done, reply:

```text
Module 23 completed
```
