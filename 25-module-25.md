# Module 25 — Working with Large Codebases in IntelliJ IDEA

## Goal
Learn how to survive and understand large enterprise codebases.

You will practice indexing awareness, entry point discovery, annotation/path searches, request flow tracing, stack trace analysis, multi-module awareness, build tool windows, dependency navigation, excluding heavy folders, and performance habits.

## Mindset

Do not try to understand everything.

First find:

```text
Entry point
Main packages
Request flow
Build system
How to run app
How to test/debug one feature
```

## First 10-Minute Checklist

```text
1. Maven, Gradle, or multi-module?
2. Where is pom.xml/build.gradle?
3. Root package?
4. Main Spring Boot class?
5. Controllers?
6. Services?
7. Repositories?
8. Config files?
9. How to run?
10. How to test one endpoint?
```

For your project:

```text
Build file       → pom.xml
Main class       → SpringbootPracticeApplication
Controllers      → controller
Services         → service
Repositories     → repository
Config           → application.properties, config
HTTP tests       → src/test/http
Docker           → docker-compose.yml
```

## Indexing

Indexing means IntelliJ reads project files and builds search/navigation data. Let indexing finish before judging performance.

## Find Entry Point

Use:

```text
Shift Shift → Application
```

Open `SpringbootPracticeApplication`.

## Identify Request Flow

```text
HTTP request
→ TaskController
→ TaskService
→ TaskRepository
→ Database
```

Open in order using Search Everywhere:

```text
TaskController
TaskService
TaskRepository
Task
TaskRequest
TaskResponse
TaskMapper
```

## Search by Annotation

Find in Files:

```text
@RestController
@Service
@Repository
@Configuration
@RequestMapping
@GetMapping
@PostMapping
@PutMapping
@DeleteMapping
```

## Search by API Path

Search:

```text
/tasks
```

Also search domain words:

```text
task
order
user
auth
payment
customer
```

## File Structure

Open `TaskController`:

```text
Cmd + F12 / Ctrl + F12
```

Jump to methods.

## Find Usages Before Changing

Use:

```text
Option + F7 / Alt + F7
```

Practice on:

```text
TaskService.createTask
TaskMapper.toResponse
TaskRepository
TaskRequest
TaskResponse
```

## Declaration/Implementation

| Action | Mac | Windows/Linux |
|---|---|---|
| Declaration | `Cmd + Click` | `Ctrl + Click` |
| Implementation | `Cmd + Option + B` | `Ctrl + Alt + B` |
| Back | `Cmd + Option + Left` | `Ctrl + Alt + Left` |

## Stack Traces

Rule:

```text
Find first line from your package: com.example.springbootpractice
```

Use:

```text
Analyze → Stack Trace or Thread Dump
```

Paste stack trace from logs/CI/Slack/Jira.

## Multi-Module Awareness

Maven example:

```text
company-platform
 ├── pom.xml
 ├── api/pom.xml
 ├── service/pom.xml
 ├── repository/pom.xml
 ├── common/pom.xml
 └── integration-tests/pom.xml
```

Always know which module contains your change.

## Maven/Gradle Tool Windows

Use to reload project, run module-specific goals, inspect dependencies, find build failures, and run focused tests.

## Exclude Heavy Folders

Possible folders:

```text
target
build
node_modules
logs
large reports
coverage output
temporary data
```

Use:

```text
Right-click folder → Mark Directory as → Excluded
```

Do not exclude source folders.

## Performance Habits

```text
1. Let indexing finish
2. Disable unused plugins
3. Exclude non-source heavy folders
4. Unload modules not needed
5. Increase memory if needed
6. Avoid huge generated files
7. Restart after plugin/config changes
```

## Investigation Scenario

Issue:

```text
POST /tasks with blank title should return 400.
```

Steps:

```text
1. Search /tasks
2. Open TaskController
3. Jump to createTask
4. Go to TaskService.createTask
5. Find validation
6. Open GlobalExceptionHandler
7. Run invalid POST
8. Debug if needed
9. Review response
```

## Notes File

Create:

```text
src/test/large-codebase-notes.md
```

```markdown
# Large Codebase Investigation Notes

## Entry Point
- Main class:

## Build System
- Maven or Gradle:

## Main Packages
- controller:
- service:
- repository:
- model:
- dto:
- config:
- exception:

## How to Run
- Run configuration:

## How to Test
- HTTP file:
- Key endpoint:

## Debug Flow
- Controller:
- Service:
- Repository:

## Common Checks
- Search by endpoint path
- Search by annotation
- Find usages before editing
- Read first stack trace line from our package
- Review Git diff before commit
```

## Assignment

```text
1. Open springboot-practice
2. Wait for indexing
3. Find main app class
4. Find TaskController
5. Search annotations
6. Search /tasks
7. Use File Structure
8. Find Usages on TaskMapper.toResponse
9. Go Controller → Service → Repository
10. Run invalid POST
11. Debug Controller → Service
12. Open Maven tool window
13. Identify build/config files
14. Review excluded folders
15. Open Analyze Stack Trace
16. Create large-codebase-notes.md
17. Fill notes
18. Review Git diff
```

When done, reply:

```text
Module 25 completed
```
