# Module 07 — Maven in IntelliJ IDEA

## Goal
Learn how to use Maven inside IntelliJ IDEA.

You will practice creating Maven project, understanding `pom.xml`, running lifecycle goals, adding dependencies, reloading Maven, and using external libraries.

## Create Maven Project

Create:

```text
maven-practice
```

Use:

```text
Maven
Java 21
Package: com.example.mavenpractice
```

## Structure

```text
maven-practice
 ├── pom.xml
 └── src
     ├── main/java
     └── test/java
```

## MavenDemo.java

```java
package com.example.mavenpractice;

public class MavenDemo {

    public static void main(String[] args) {
        System.out.println("Maven project is running in IntelliJ IDEA.");
    }
}
```

## Maven Tool Window

Open:

```text
View → Tool Windows → Maven
```

Lifecycle goals:

```text
clean
compile
test
package
install
```

Run clean, compile, package.

## Add Dependency

In `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.14.0</version>
</dependency>
```

Click Load Maven Changes.

## StringCheckDemo.java

```java
package com.example.mavenpractice;

import org.apache.commons.lang3.StringUtils;

public class StringCheckDemo {

    public static void main(String[] args) {
        String value = "   ";

        if (StringUtils.isBlank(value)) {
            System.out.println("Value is blank");
        } else {
            System.out.println("Value is not blank");
        }
    }
}
```

Expected:

```text
Value is blank
```

## Maven Commands

```bash
mvn clean compile
mvn test
mvn package
mvn -U clean package
```

`-U` forces Maven to retry dependency downloads.

## Assignment

```text
1. Create maven-practice
2. Create MavenDemo
3. Run MavenDemo
4. Open Maven tool window
5. Run clean, compile, package
6. Add commons-lang3
7. Reload Maven
8. Create StringCheckDemo
9. Run StringCheckDemo
10. Check External Libraries
```

When done, reply:

```text
Module 7 completed
```
