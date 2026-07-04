# Module 15 — IntelliJ HTTP Client Deep Dive

## Goal
Use IntelliJ HTTP Client like a repeatable API testing tool.

You will practice `.http` files, request names, environments, private environment files, CRUD organization, response validation scripts, cURL conversion, request generation, request history, and Git-safe setup.

## Advanced HTTP File

Create:

```text
src/test/http/task-api-advanced.http
```

## Environment File

Create:

```text
src/test/http/http-client.env.json
```

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

## Private Environment File

Create:

```text
src/test/http/http-client.private.env.json
```

Example:

```json
{
  "local": {
    "token": "do-not-commit-real-token"
  }
}
```

Add to `.gitignore`:

```gitignore
http-client.private.env.json
**/http-client.private.env.json
```

## Full CRUD Requests

```http
### Get all tasks
# @name getAllTasks
GET {{baseUrl}}/tasks

### Get task by ID
# @name getTaskById
GET {{baseUrl}}/tasks/{{taskId}}

### Create task
# @name createTask
POST {{baseUrl}}/tasks
Content-Type: application/json

{
  "title": "Created from IntelliJ HTTP Client",
  "status": "OPEN"
}

### Update task
# @name updateTask
PUT {{baseUrl}}/tasks/{{taskId}}
Content-Type: application/json

{
  "title": "Updated from IntelliJ HTTP Client",
  "status": "COMPLETED"
}

### Delete task
# @name deleteTask
DELETE {{baseUrl}}/tasks/{{taskId}}
```

## Response Validation

```http
> {%
    client.test("Status is 200", function () {
        client.assert(response.status === 200, "Expected status 200");
    });
%}
```

## Invalid Request Example

```http
### Create invalid task
# @name createInvalidTask
POST {{baseUrl}}/tasks
Content-Type: application/json

{
  "title": "",
  "status": "OPEN"
}

> {%
    client.test("Invalid task behavior reviewed", function () {
        client.assert(response.status === 400 || response.status === 200, "Review validation behavior");
    });
%}
```

## cURL Conversion

Paste cURL:

```bash
curl -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"From curl","status":"OPEN"}'
```

IntelliJ can convert/suggest HTTP format.

## Request History

Use Find Action:

```text
HTTP Requests
HTTP Client
Show HTTP Requests
```

## Assignment

```text
1. Create task-api-advanced.http
2. Create http-client.env.json
3. Create private env file
4. Add private env to .gitignore
5. Add GET/POST/PUT/DELETE requests
6. Use {{baseUrl}} and {{taskId}}
7. Add validation script
8. Run all requests
9. Try cURL conversion
10. Try request generation from controller
11. Review request history
12. Commit only safe files
```

When done, reply:

```text
Module 15 completed
```
