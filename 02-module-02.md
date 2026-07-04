# Module 02 — IntelliJ Navigation Basics

## Goal
Learn how to move around a project quickly without manually clicking folders.

You will practice Search Everywhere, Go to Class, Go to File, Recent Files, Go to Declaration, Find Usages, Terminal, and navigation history.

## Create Practice Package

Create:

```text
com.example.navigation
```

Create classes:

```text
Customer
Order
Payment
NavigationApp
```

## Customer.java

```java
package com.example.navigation;

public class Customer {

    private String name;

    public Customer(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

## Order.java

```java
package com.example.navigation;

public class Order {

    private String itemName;
    private Customer customer;

    public Order(String itemName, Customer customer) {
        this.itemName = itemName;
        this.customer = customer;
    }

    public String getItemName() {
        return itemName;
    }

    public Customer getCustomer() {
        return customer;
    }
}
```

## Payment.java

```java
package com.example.navigation;

public class Payment {

    public void pay(Order order) {
        System.out.println("Paid for: " + order.getItemName());
        System.out.println("Customer: " + order.getCustomer().getName());
    }
}
```

## NavigationApp.java

```java
package com.example.navigation;

public class NavigationApp {

    public static void main(String[] args) {
        Customer customer = new Customer("Nithakanan");
        Order order = new Order("IntelliJ IDEA Course", customer);

        Payment payment = new Payment();
        payment.pay(order);
    }
}
```

Expected output:

```text
Paid for: IntelliJ IDEA Course
Customer: Nithakanan
```

## Search Everywhere

| OS | Shortcut |
|---|---|
| Mac | `Shift` `Shift` |
| Windows/Linux | `Shift` `Shift` |

Search and open:

```text
Customer
Order
Payment
NavigationApp
```

## Go to Class

| OS | Shortcut |
|---|---|
| Mac | `Cmd + O` |
| Windows/Linux | `Ctrl + N` |

Search `Payment`.

## Go to File

| OS | Shortcut |
|---|---|
| Mac | `Cmd + Shift + O` |
| Windows/Linux | `Ctrl + Shift + N` |

Search `NavigationApp.java`.

## Recent Files

| OS | Shortcut |
|---|---|
| Mac | `Cmd + E` |
| Windows/Linux | `Ctrl + E` |

Use this to switch between files instead of clicking tabs.

## Go to Declaration

In `NavigationApp.java`, use:

| OS | Shortcut |
|---|---|
| Mac | `Cmd + Click` |
| Windows/Linux | `Ctrl + Click` |

Click `Customer`, `Order`, `Payment`, and `pay`.

## Find Usages

| OS | Shortcut |
|---|---|
| Mac | `Option + F7` |
| Windows/Linux | `Alt + F7` |

Try on `Customer`, `Order`, `Payment.pay`, and `getName`.

## Back and Forward

| Action | Mac | Windows/Linux |
|---|---|---|
| Back | `Cmd + Option + Left` | `Ctrl + Alt + Left` |
| Forward | `Cmd + Option + Right` | `Ctrl + Alt + Right` |

## Terminal

| OS | Shortcut |
|---|---|
| Mac | `Option + F12` |
| Windows/Linux | `Alt + F12` |

Run:

```bash
pwd
ls
```

## Assignment

```text
1. Create com.example.navigation
2. Create Customer, Order, Payment, NavigationApp
3. Run NavigationApp
4. Open each class using Shift Shift
5. Open Customer using Go to Class
6. Open NavigationApp.java using Go to File
7. Use Recent Files
8. Use Go to Declaration
9. Use Find Usages on Customer
10. Open Terminal
```

When done, reply:

```text
Module 2 completed
```
