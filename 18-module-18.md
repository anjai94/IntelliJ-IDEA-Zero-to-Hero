# Module 18 — Docker and Local Development

## Goal
Use Docker with IntelliJ to run PostgreSQL locally and connect Spring Boot to it.

You will practice Docker plugin/connection, `docker-compose.yml`, containers in Services, PostgreSQL dependency, datasource config, Database tool window, SQL verification, and secret safety.

## Check Docker

Make sure Docker Desktop is running.

IntelliJ:

```text
Settings → Build, Execution, Deployment → Docker
```

## docker-compose.yml

Create at project root:

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

## Start Container

From IntelliJ gutter or terminal:

```bash
docker compose up -d
docker ps
```

## Add PostgreSQL Dependency

```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
</dependency>
```

Reload Maven.

## application.properties for PostgreSQL

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

Run app. Expected JDBC URL should show PostgreSQL.

## Test API

```http
GET http://localhost:8080/tasks
```

```http
POST http://localhost:8080/tasks
Content-Type: application/json

{
  "title": "Stored in PostgreSQL",
  "status": "OPEN"
}
```

## Database Tool Window

```text
View → Tool Windows → Database
+ → Data Source → PostgreSQL
```

Use:

```text
Host: localhost
Port: 5432
Database: taskdb
User: taskuser
Password: taskpass
```

SQL:

```sql
SELECT * FROM task;
```

## Stop Containers

Keep data:

```bash
docker compose down
```

Delete data:

```bash
docker compose down -v
```

## Security Habit

Learning credentials are okay for local practice. Real project credentials must not be committed.

## Assignment

```text
1. Verify Docker Desktop
2. Configure Docker in IntelliJ
3. Create docker-compose.yml
4. Start PostgreSQL
5. Add PostgreSQL dependency
6. Reload Maven
7. Configure application.properties
8. Run Spring Boot
9. Test GET/POST
10. Add PostgreSQL datasource in IntelliJ
11. Run SELECT * FROM task
12. Stop/start container and verify data persists
```

When done, reply:

```text
Module 18 completed
```
