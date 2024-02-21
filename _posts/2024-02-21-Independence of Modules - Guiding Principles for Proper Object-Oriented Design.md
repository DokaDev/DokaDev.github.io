---
title: Independence of Modules - Guiding Principles for Proper Object-Oriented Design
date: 2024-02-21 09:43:00 +0900
categories: [Object Oriented]
math: true
tags: [oop]     # TAG names should always be lowercase
---
Learning Object-Oriented Programming(OOP) is different from studying the syntax of a programming language. It is about understanding the methods for designing software correctly. Proper software design aims for easy maintenance, high extensibility, and reusable code. To achieve these design goals, Object-Oriented Programming provides core concepts such as classes, inheritance, polymorphism, and encapsulation.

Furthermore, Object-Oriented Programming offers solutions to many problems that can arise during the software development process. For instance, using inheritance and polymorphism can reduce code duplication and increase flexibility. Encapsulation allows the internal implementation of an object to be changed without affecting other objects, ensuring that even if only a part of the system is modified, the whole system remains stable.

In conclusion, learning Object-Oriented Programming is more than just understanding the grammar of a language; it is about acquiring the skills to create well-designed software. This forms an essential foundation that enables developers to develop better software more efficiently. Therefore, understanding and correctly the principles of object oriented is a critical skill that all software developers must possess.



## Concept and Independence of Modules

One of the essential concepts for proper software design is **modularization**. Modularization refers to the process of breaking down a complex system into manageable small units. Through this process, each module performs a limited and independent function, and each module interacts with others through clearly defined interfaces. This makes the software more flexible, reusable, and extensible.

Here, a **module** refers to a bundle of code that performs a specific function in software design. A module can take various forms, such as functions, classes, or packages. Modularization makes it easier to solve large problems by breaking them down into smaller units.

```c
// This can also be seen as a module.
int main() {
    return;
}
```

For proper modularization, modules are divided according to the function they are intended to perform, making each module perform a given function independently. This means that each module has less dependency on external elements, which is expressed as having **high independence of modules**. The higher the independence, the less it is affected by changes in other parts, making maintenance easier.

The independence of a module can be evaluated through the following two indicators:

* **Coupling**: The degree of dependency between modules.
* **Cohesion**: The degree of relatedness among the components within a module.

Well-designed software tends to have high module in independence, characterized by high cohesion and low coupling. In other words, the higher the cohesion and the lower the coupling, the higher the independence of a module can be considered.



## Coupling

Coupling is a measure of the degree of dependency between modules. The lower the coupling, the more independently each module operates, making changes and maintenance easier. In other words, changes in one module have less impact on others. This is closely related to the **DIP(Dependency Inversion Principle)** and **ISP(Interface Segregation Principle)** that will be discussed in future posts.

* **DIP**: High-level modules should not depend on low-level modules; both should depend on abstractions. This allows for basing designs on abstractions rather than concrete implementations, thereby reducing coupling.
* **ISP**: Interfaces should not force the implementation of unused methods. This allows a class not to depend on methods it does not use, thereby reducing coupling.

From the perspective of Object-Oriented Programming, coupling evaluates whether modules, such as classes and methods, maintain only the necessary level of relationships required for cooperation.

Therefore, it can be said that good software has low coupling.

Coupling is divided into the following six levels, with higher levels of coupling as we progress:

* **Data Coupling**
* **Stamp Coupling**
* **Control Coupling**
* **External Coupling**
* **Common Coupling**
* **Content Coupling**



### Data Coupling

It represents the lowest level of coupling, as shown in the code below, where modules only pass data between them, and the called module is only affected through parameters.

```java
class DataCouplingExample {
    void displayMessage(String message) {
        System.out.println(message);
    }
    
    void execute() {
        displayMessage("Hello, Data Coupling!");
    }
}
```



### Stamp Coupling

This refers to the passing of structured data, like objects, between modules, rather than simple data.

```java
class User {
    String name;
    int age;

    User(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

class StampCouplingExample {
    void displayUser(User user) {
        System.out.println("User: " + user.name + ", Age: " + user.age);
    }

    void execute() {
        User user = new User("John Doe", 30);
        displayUser(user);
    }
}
```



### Control Coupling

Occurs when one module controls the flow of another by passing control information.

```java
class ControlCouplingExample {
    void display(String message, boolean uppercase) {
        if (uppercase) {
            System.out.println(message.toUpperCase());
        } else {
            System.out.println(message);
        }
    }

    void execute() {
        display("Hello, Control Coupling!", true);
    }
}
```



### External Coupling

Occurs when two or more modules depend on external factors like global variables or external file systems. The following code uses a system's environment variable as an example.

```java
class ExternalCouplingExample {
    void readSystemConfig() {
        String dbUrl = System.getenv("DATABASE_URL");
        System.out.println("Database URL: " + dbUrl);
    }
}
```



### Common Coupling

Occurs when multiple modules share the same global data, such as using a common data area like global variables.

```java
class GlobalData {
    static int globalValue = 10;
}

class CommonCouplingExample {
    void incrementGlobalValue() {
        GlobalData.globalValue++;
    }

    void displayGlobalValue() {
        System.out.println("Global Value: " + GlobalData.globalValue);
    }
}
```



### Content Coupling

Occurs when one modules directly refers to or modifies the internal working of another module. It is the highest level of coupling and should be avoided.

> Providing a direct example is contrary to standard programming practices, but for educational purposes, a simple example is given. Please remember not to use this design in actual development environments.
{: .prompt-danger }

An example is the use of Java reflection to access a class's private fields or methods. Although Java's reflection API allows accessing or calling a class's private fields or methods, this design has very high coupling because it directly depends on the class's internal implementation.

```java
import java.lang.reflect.Field;

class PrivateData {
    private String secret = "This is a secret message";
}

public class ContentCouplingExample {
    public static void main(String[] args) throws Exception {
        PrivateData data = new PrivateData();
        
        // Directly accessing the 'secret' private field of the PrivateData class
        Field field = PrivateData.class.getDeclaredField("secret");
        field.setAccessible(true); // Making it accessible
        String secretValue = (String) field.get(data);
        
        System.out.println("Accessed secret value: " + secretValue);
    }
}
```



---

## Cohesion

Cohesion measures how closely related and focused the components within a module are. The higher the cohesion, the more focused a module is on a single purpose or task. This means that when a feature needs to be modified, related content is grouped within a module, making the code easier to understand and modify without affecting unnecessary modules, thereby facilitating maintenance. 

High cohesion design principles are directly related to the **SRP(Single Responsibility Principle)** in the **SOLID principles**.

* **SRP**: A design element(module, class, functions, etc.) should have only one reason to change, ensuring high cohesion.

Thus, the higher the cohesion, the more independent a module is, and good software maintains high cohesion.

Cohesion is divided into the following seven levels, with lower levers of cohesion as we progress:

* **Functional Cohesion**
* **Sequential Cohesion**
* **Communication Cohesion**
* **Procedural Cohesion**
* **Temporal Cohesion**
* **Logical Cohesion**
* **Coincidental Cohesion**



### Functional Cohesion

Occurs when all elements within a module are grouped to perform a single task, representing the ideal level of cohesion.

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    int subtract(int a, int b) {
        return a - b;
    }

    int multiply(int a, int b) {
        return a * b;
    }

    int divide(int a, int b) {
        if (b == 0) throw new ArithmeticException("Cannot divide by zero");
        return a / b;
    }
}
```



### Sequential Cohesion

Occurs when the elements within a module are required to be executed in a specific order, where the output of one element becomes the input of the next.

```java
class SequentialProcess {
    String readData() {
        return "data";
    }

    String processData(String data) {
        return "processed " + data;
    }

    void saveData(String data) {
        System.out.println("Saving " + data);
    }

    void execute() {
        String data = readData();
        String processed = processData(data);
        saveData(processed);
    }
}
```



### Communicational Cohesion

Occurs when elements within a module use the same input and produce the same output but perform different tasks.

```java
class ReportGenerator {
    void generateHeader(String reportType) {
        System.out.println("Header for " + reportType);
    }

    void generateBody(String data) {
        System.out.println("Body with data " + data);
    }

    void generateFooter(String reportType) {
        System.out.println("Footer for " + reportType);
    }

    void execute() {
        String data = "Annual Report Data";
        generateHeader("Annual");
        generateBody(data);
        generateFooter("Annual");
    }
}
```



### Procedural Cohesion

Occurs when elements within a module are grouped because they contribute to a single task through different steps or procedures.

```java
class UserProcess {
    void login(String user) {
        System.out.println(user + " logged in");
    }

    void accessData(String user) {
        System.out.println(user + " accessed data");
    }

    void logout(String user) {
        System.out.println(user + " logged out");
    }

    void executeProcess(String user) {
        login(user);
        accessData(user);
        logout(user);
    }
}
```



### Temporal Cohesion

Occurs when elements within a module are grouped to be executed at the same time, such as initialization and termination tasks.

```java
class ApplicationLifecycle {
    void start() {
        System.out.println("Application starting");
    }

    void initialize() {
        System.out.println("Initializing application");
    }

    void stop() {
        System.out.println("Application stopping");
    }

    void executeLifecycle() {
        start();
        initialize();
        stop();
    }
}
```



### Logical Cohesion

Occurs when elements within a module are logically similar but perform different tasks, grouped together based on logical relationships.

```java
class TaskExecutor {
    void executeTask(String taskType) {
        switch (taskType) {
            case "clean":
                System.out.println("Cleaning");
                break;
            case "build":
                System.out.println("Building");
                break;
            case "deploy":
                System.out.println("Deploying");
                break;
            default:
                System.out.println("Unknown task");
        }
    }
}
```



### Coincidental Cohesion

Occurs when elements within a module are unrelated, representing the lowest the lowerr level of cohesion and a design to be avoided.

```java
class MiscellaneousTasks {
    void task1() {
        System.out.println("Performing task1");
    }

    void task2() {
        System.out.println("Performing task2");
    }

    void task3() {
        System.out.println("Performing task3");
    }
}
```



Understanding Object-Oriented Programming, modularization, and the concepts of coupling and cohesion transcends simple programming techniques. These principles offer a fundamental approach to how we design and effectively manage software. They are invaluable in designing and maintaining complex systems, helping to solve various issues that may arise. Specifically, designing for low coupling and high cohesion is key to building flexible and scalable software architectures. This ensures sustainable software development even as requirements and technological environments changes.

As software developers, we must always keep these principles in mind, actively applying them during the design and implementation phrases. Continuous learning and practice are required to internalize these principles and strive to become better software designers.
