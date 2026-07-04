# Module 05 — Running Applications and Run Configurations

## Goal
Learn how IntelliJ runs applications and how to configure run behavior.

You will practice running classes, editing run configurations, passing program arguments, passing environment variables, creating dev/prod-like configurations, and understanding Run output.

## Package

```text
com.example.runconfig
```

Create:

```text
RunDemo
ArgumentDemo
EnvironmentDemo
```

## RunDemo.java

```java
package com.example.runconfig;

public class RunDemo {

    public static void main(String[] args) {
        System.out.println("Application is running from IntelliJ IDEA.");
    }
}
```

## ArgumentDemo.java

```java
package com.example.runconfig;

public class ArgumentDemo {

    public static void main(String[] args) {
        System.out.println("Number of arguments: " + args.length);

        for (String arg : args) {
            System.out.println("Argument: " + arg);
        }
    }
}
```

Run without arguments. Then open:

```text
Run → Edit Configurations
```

Set Program arguments:

```text
dev 8080 enabled
```

Expected:

```text
Number of arguments: 3
Argument: dev
Argument: 8080
Argument: enabled
```

## EnvironmentDemo.java

```java
package com.example.runconfig;

public class EnvironmentDemo {

    public static void main(String[] args) {
        String appMode = System.getenv("APP_MODE");
        String appUser = System.getenv("APP_USER");

        System.out.println("APP_MODE = " + appMode);
        System.out.println("APP_USER = " + appUser);
    }
}
```

Set environment variables:

```text
APP_MODE=local;APP_USER=Nithakanan
```

Expected:

```text
APP_MODE = local
APP_USER = Nithakanan
```

## Create Multiple Configurations

Local:

```text
EnvironmentDemo - Local
APP_MODE=local;APP_USER=Nithakanan
```

Production simulation:

```text
EnvironmentDemo - Prod Simulation
APP_MODE=prod;APP_USER=prod-user
```

Never use real production secrets in local run configurations.

## Important Fields

```text
Main class
Program arguments
Environment variables
Working directory
JDK
Module classpath
```

## Shortcuts

| Action | Mac | Windows/Linux |
|---|---|---|
| Run | `Ctrl + R` | `Shift + F10` |
| Debug | `Ctrl + D` | `Shift + F9` |
| Stop | `Cmd + F2` | `Ctrl + F2` |
| Terminal | `Option + F12` | `Alt + F12` |

## Assignment

```text
1. Create RunDemo and run it
2. Create ArgumentDemo
3. Run without arguments
4. Add program arguments
5. Create EnvironmentDemo
6. Add APP_MODE and APP_USER env vars
7. Create Local and Prod Simulation configurations
8. Rename one run configuration
9. Duplicate one run configuration
```

When done, reply:

```text
Module 5 completed
```
