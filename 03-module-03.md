# Module 03 — Writing Code Faster

## Goal
Learn IntelliJ features that help you write Java code faster and with fewer mistakes.

You will practice code completion, Generate constructor/getters/setters/toString, auto-import, reformat, duplicate/delete/move lines, live templates, postfix completion, and Quick Fix.

## Create Package

```text
com.example.fastcoding
```

Create:

```text
Product
Order
Payment
ShopApp
```

## Product.java

Start with fields:

```java
package com.example.fastcoding;

public class Product {

    private String name;
    private double price;
    private int quantity;

}
```

Use Generate Code:

| OS | Shortcut |
|---|---|
| Mac | `Cmd + N` |
| Windows/Linux | `Alt + Insert` |

Generate constructor, getters, setters, and `toString`.

Final version:

```java
package com.example.fastcoding;

public class Product {

    private String name;
    private double price;
    private int quantity;

    public Product(String name, double price, int quantity) {
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public int getQuantity() {
        return quantity;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }

    public double getTotalPrice() {
        return price * quantity;
    }

    @Override
    public String toString() {
        return "Product{name='" + name + "', price=" + price + ", quantity=" + quantity + "}";
    }
}
```

## Order.java

```java
package com.example.fastcoding;

public class Order {

    private Product product;
    private String customerName;

    public Order(Product product, String customerName) {
        this.product = product;
        this.customerName = customerName;
    }

    public void printSummary() {
        System.out.println("Customer: " + customerName);
        System.out.println("Product: " + product.getName());
        System.out.println("Total: " + product.getTotalPrice());
    }
}
```

## Payment.java

```java
package com.example.fastcoding;

public class Payment {

    public void processPayment(Order order) {
        System.out.println("Payment processed successfully.");
    }
}
```

## ShopApp.java

```java
package com.example.fastcoding;

public class ShopApp {

    public static void main(String[] args) {
        Product product = new Product("Laptop", 1200.00, 2);
        Order order = new Order(product, "Nithakanan");

        order.printSummary();

        Payment payment = new Payment();
        payment.processPayment(order);
    }
}
```

Expected output:

```text
Customer: Nithakanan
Product: Laptop
Total: 2400.0
Payment processed successfully.
```

## Shortcuts

| Action | Mac | Windows/Linux |
|---|---|---|
| Basic completion | `Ctrl + Space` | `Ctrl + Space` |
| Smart completion | `Ctrl + Shift + Space` | `Ctrl + Shift + Space` |
| Generate code | `Cmd + N` | `Alt + Insert` |
| Quick Fix | `Option + Enter` | `Alt + Enter` |
| Reformat | `Cmd + Option + L` | `Ctrl + Alt + L` |
| Optimize imports | `Ctrl + Option + O` | `Ctrl + Alt + O` |
| Line comment | `Cmd + /` | `Ctrl + /` |
| Duplicate line | `Cmd + D` | `Ctrl + D` |
| Delete line | `Cmd + Delete` | `Ctrl + Y` |

## Live Templates

```text
psvm → public static void main
sout → System.out.println
soutv → print variable
soutp → print parameters
soutm → print method
```

## Assignment

```text
1. Create com.example.fastcoding
2. Create Product, Order, Payment, ShopApp
3. Generate constructor/getters/setters/toString
4. Run ShopApp
5. Practice duplicate/delete/move line
6. Practice comments
7. Practice psvm and sout
8. Use Quick Fix 3 times
9. Reformat all files
10. Optimize imports
```

When done, reply:

```text
Module 3 completed
```
