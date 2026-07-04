# Module 08 — Gradle in IntelliJ IDEA

## Goal
Learn how to use Gradle inside IntelliJ IDEA.

You will practice creating Gradle project, understanding `build.gradle`, running tasks, adding dependencies, reloading Gradle, and using Gradle wrapper.

## Create Gradle Project

Create:

```text
gradle-practice
```

Use:

```text
Gradle
Java
JDK 21
Package: com.example.gradlepractice
```

## Structure

```text
gradle-practice
 ├── build.gradle
 ├── settings.gradle
 ├── gradlew
 ├── gradlew.bat
 └── src/main/java
```

## GradleDemo.java

```java
package com.example.gradlepractice;

public class GradleDemo {

    public static void main(String[] args) {
        System.out.println("Gradle project is running in IntelliJ IDEA.");
    }
}
```

## Gradle Tool Window

Open:

```text
View → Tool Windows → Gradle
```

Run tasks:

```text
clean
build
test
jar
```

## Add Dependency

In `build.gradle`:

```groovy
dependencies {
    implementation 'org.apache.commons:commons-lang3:3.14.0'
    testImplementation platform('org.junit:junit-bom:5.10.0')
    testImplementation 'org.junit.jupiter:junit-jupiter'
}
```

Reload Gradle.

## GradleStringCheckDemo.java

```java
package com.example.gradlepractice;

import org.apache.commons.lang3.StringUtils;

public class GradleStringCheckDemo {

    public static void main(String[] args) {
        String value = "";

        if (StringUtils.isBlank(value)) {
            System.out.println("Blank value detected from Gradle project.");
        }
    }
}
```

## Gradle Wrapper

Mac/Linux:

```bash
./gradlew clean build
```

Windows:

```bash
gradlew.bat clean build
```

Wrapper keeps Gradle version consistent across machines.

## Assignment

```text
1. Create gradle-practice
2. Create GradleDemo
3. Run GradleDemo
4. Open Gradle tool window
5. Run clean and build
6. Add commons-lang3
7. Reload Gradle
8. Create GradleStringCheckDemo
9. Run it
10. Run ./gradlew clean build
```

When done, reply:

```text
Module 8 completed
```
