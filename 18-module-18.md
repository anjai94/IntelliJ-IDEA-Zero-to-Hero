# Module 18 — Docker and Local Development Using Community Edition

## Goal

In this module, you will learn how to use Docker with IntelliJ IDEA **Community Edition**.

Because you are using **Community Edition**, we will **not depend on IntelliJ Docker Services / Docker tool window**. Instead, we will use:

```text
IntelliJ Terminal
docker command
docker compose command
docker-compose.yml file
Spring Boot application.properties
curl/browser testing
psql inside Docker container
```

This is actually a very good real-world workflow.

---

## 1. What You Will Build

You will run a PostgreSQL database using Docker, then connect your Spring Boot app to it.

Current flow:

```text
Spring Boot API
   ↓
Spring Data JPA
   ↓
PostgreSQL running in Docker
```

---

## 2. Check Docker Is Installed

Open IntelliJ Terminal:

```text
View → Tool Windows → Terminal
```

or shortcut:

| Mac | Windows/Linux |
|---|---|
| `Option + F12` | `Alt + F12` |

Run:

```bash
docker --version
```

Expected example:

```text
Docker version 27.x.x
```

Then run:

```bash
docker compose version
```

Expected example:

```text
Docker Compose version v2.x.x
```

If these commands fail, Docker Desktop is not running or not installed.

---

## 3. Create `docker-compose.yml`

In your Spring Boot project root, same level as `pom.xml`, create:

```text
docker-compose.yml
```

Paste:

```yaml
services:
  postgres:
    image: postgres:16
    container_name: task-postgres
    environment:
      POSTGRES_DB: taskdb
      POSTGRES_USER: taskuser
      POSTGRES_PASSWORD: taskpass
    ports:
      - "5432:5432"
    volumes:
      - task-postgres-data:/var/lib/postgresql/data

volumes:
  task-postgres-data:
```

Your project should look like:

```text
springboot-practice
 ├── pom.xml
 ├── docker-compose.yml
 └── src
```

---

## 4. Understand the Docker Compose File

```yaml
image: postgres:16
```

This means Docker will download PostgreSQL version 16.

```yaml
container_name: task-postgres
```

This is the container name.

```yaml
POSTGRES_DB: taskdb
POSTGRES_USER: taskuser
POSTGRES_PASSWORD: taskpass
```

These create the database and login credentials.

```yaml
ports:
  - "5432:5432"
```

This exposes PostgreSQL to your Mac/PC on port `5432`.

```yaml
volumes:
  - task-postgres-data:/var/lib/postgresql/data
```

This keeps database data even if the container stops.

---

## 5. Start PostgreSQL Container

In IntelliJ Terminal, run:

```bash
docker compose up -d
```

Meaning:

```text
up = start containers
-d = detached mode / run in background
```

Expected output:

```text
Container task-postgres Started
```

Check running containers:

```bash
docker ps
```

You should see:

```text
task-postgres
postgres:16
0.0.0.0:5432->5432/tcp
```

---

## 6. View PostgreSQL Logs

Run:

```bash
docker logs task-postgres
```

You should see PostgreSQL startup logs.

If it says something like:

```text
database system is ready to accept connections
```

PostgreSQL is ready.

---

## 7. Add PostgreSQL Dependency to `pom.xml`

Open `pom.xml`.

Add this inside `<dependencies>`:

```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
</dependency>
```

Keep your existing dependencies, for example:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

Then click:

```text
Load Maven Changes
```

or run:

```bash
mvn clean package
```

If Maven has download issues, run:

```bash
mvn -U clean package
```

Remember:

```text
-U = force Maven to retry dependency downloads
```

---

## 8. Update `application.properties`

Open:

```text
src/main/resources/application.properties
```

For PostgreSQL, use:

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

Important: this will switch your app from H2 to PostgreSQL.

---

## 9. Run Spring Boot App

Run:

```text
SpringbootPracticeApplication
```

In Community Edition, just run the main class like a normal Java application.

Expected logs should show something similar to:

```text
Tomcat started on port 8080
Database JDBC URL [jdbc:postgresql://localhost:5432/taskdb]
Started SpringbootPracticeApplication
```

You should **not** see:

```text
jdbc:h2:mem:taskdb
```

If you still see H2, your `application.properties` is not using PostgreSQL correctly.

---

## 10. Test API with curl

Run:

```bash
curl http://localhost:8080/tasks
```

Expected: JSON task list.

Create a task:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Task saved in PostgreSQL Docker","status":"OPEN"}'
```

Then check again:

```bash
curl http://localhost:8080/tasks
```

---

## 11. Connect to PostgreSQL from Terminal

Run:

```bash
docker exec -it task-postgres psql -U taskuser -d taskdb
```

You are now inside PostgreSQL.

Run:

```sql
SELECT * FROM task;
```

Expected: you should see rows from your Spring Boot API.

Example:

```text
 id | status | title
----+--------+-------------------------------
  1 | OPEN   | Task saved in PostgreSQL Docker
```

Exit PostgreSQL:

```sql
\q
```

---

## 12. Useful Docker Commands

### Start containers

```bash
docker compose up -d
```

### Stop containers

```bash
docker compose down
```

### Stop and delete database volume

Be careful. This deletes the database data.

```bash
docker compose down -v
```

### Check running containers

```bash
docker ps
```

### Check all containers

```bash
docker ps -a
```

### View logs

```bash
docker logs task-postgres
```

### Restart container

```bash
docker restart task-postgres
```

---

## 13. Debug with PostgreSQL

Set breakpoint in:

```text
TaskController.createTask
TaskService.createTask
TaskRepository.save
```

Run app in Debug mode.

Send request:

```bash
curl -i -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Debug PostgreSQL save","status":"OPEN"}'
```

In debugger, inspect:

```text
task.title
task.status
saved task id
```

Then check DB:

```bash
docker exec -it task-postgres psql -U taskuser -d taskdb
```

```sql
SELECT * FROM task;
```

---

## 14. Community Edition Important Note

In IntelliJ IDEA Ultimate, you may see Docker and Database tool windows.

But in **Community Edition**, use:

| Need | Community Edition Method |
|---|---|
| Start PostgreSQL | `docker compose up -d` |
| Stop PostgreSQL | `docker compose down` |
| View DB logs | `docker logs task-postgres` |
| Open DB shell | `docker exec -it task-postgres psql -U taskuser -d taskdb` |
| Test API | `curl`, browser, Postman |
| Debug app | Standard Java debugger |
| Check SQL | `psql` terminal |

This is enough for real development.

---

## 15. Common Issues

### Issue 1 — Port 5432 already in use

Error may look like:

```text
Bind for 0.0.0.0:5432 failed: port is already allocated
```

Fix option 1: stop existing PostgreSQL.

```bash
docker ps
```

Stop old container:

```bash
docker stop <container-id>
```

Fix option 2: change port in `docker-compose.yml`:

```yaml
ports:
  - "5433:5432"
```

Then update `application.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5433/taskdb
```

---

### Issue 2 — Password authentication failed

Check these match exactly.

In `docker-compose.yml`:

```yaml
POSTGRES_USER: taskuser
POSTGRES_PASSWORD: taskpass
POSTGRES_DB: taskdb
```

In `application.properties`:

```properties
spring.datasource.username=taskuser
spring.datasource.password=taskpass
spring.datasource.url=jdbc:postgresql://localhost:5432/taskdb
```

If you changed username/password after the volume was already created, run:

```bash
docker compose down -v
docker compose up -d
```

Warning: `-v` deletes database data.

---

### Issue 3 — App still uses H2

Check your logs.

If you see:

```text
jdbc:h2:mem:taskdb
```

then PostgreSQL config is not active.

Check:

```text
application.properties
```

Make sure PostgreSQL properties are saved.

Restart the app.

---

### Issue 4 — Table not found

Check this setting:

```properties
spring.jpa.hibernate.ddl-auto=update
```

Then restart app.

Hibernate should create/update the table.

---

### Issue 5 — Docker command not found

Check Docker Desktop is installed and running.

Run:

```bash
docker --version
```

If it fails, restart Docker Desktop.

---

## 16. Optional: Use DBeaver

Since Community Edition may not include IntelliJ Database tools, you can use **DBeaver** as a free external database client.

Connection values:

```text
Host: localhost
Port: 5432
Database: taskdb
Username: taskuser
Password: taskpass
```

But this is optional. `psql` inside Docker is enough for this course.

---

## 17. Final Check

Before completing this module, confirm:

```text
Docker container is running
Spring Boot connects to PostgreSQL
GET /tasks works
POST /tasks saves data
psql SELECT * FROM task shows saved rows
You can stop/start Docker container
You can debug POST /tasks
```

---

## Module 18 Assignment

Complete these tasks:

```text
1. Open springboot-practice
2. Create docker-compose.yml
3. Add PostgreSQL container configuration
4. Run docker compose up -d
5. Confirm container is running with docker ps
6. Add PostgreSQL dependency to pom.xml
7. Reload Maven
8. Update application.properties for PostgreSQL
9. Run Spring Boot main class
10. Confirm logs show PostgreSQL JDBC URL
11. Test GET /tasks using curl
12. Test POST /tasks using curl
13. Connect to PostgreSQL using docker exec and psql
14. Run SELECT * FROM task;
15. Debug POST /tasks
16. Stop PostgreSQL using docker compose down
17. Start PostgreSQL again
18. Confirm data still exists
19. Review Git diff
20. Commit with message:
    Add PostgreSQL Docker setup for local development
```

When done, reply:

```text
Module 18 completed
```
