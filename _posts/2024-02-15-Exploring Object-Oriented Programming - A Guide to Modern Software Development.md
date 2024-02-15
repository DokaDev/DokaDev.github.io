---
title: Exploring Object-Oriented Programming - A Guide to Modern Software Development
date: 2024-02-15 16:03:00 +0900
image: 
    path: /assets/post/object/0.png
    alt: The cover image is created by DALL-E
categories: [Object Oriented]
tags: [oop]     # TAG names should always be lowercase
---

The realm of programming is filled with various paradigms, yet the most commonly contrasted are procedural programming and object-oriented programming(OOP). Grasping the fundamental differences between these two is crucial for understanding the fundamental approaches to programming.



## Procedural Programming

Procedural programming views a program as a sequence of steps or procedures. The focus here is on "what to do" and "in what order to do it". Simply put, a program is perceived as a collection of commands that are executed in logical order. This approach is beneficial for developing small-scale programs or single tasks quickly but faces maintainability and scalability challenges as complexity grows.



## Object-Oriented Programming(OOP)

Conversely, object-oriented programming conceptualizes a program as a collection of objects. An object includes data (attributes) and methods (functions) for processing the data. The essence of OOP lies in structuring programs and encapsulating data. The method significantly enhances a program's reusability, scalability, and maintainability.



### Core Features of OOP

#### Abstraction

Abstraction is the process of simplifying the complex real world into a manageable model within the program. This allows developers to focus on the essential characteristics and behaviors of an object without worrying about the complex details of its implementation.

> Take a car, for example.
>
> A real car consists of numerous components like the engine, wheels, and transmission, but in programming, it can be modeled as a car object with methods like 'drive' and 'stop'.
>
> Selecting only the necessary attributes and methods to define is what abstraction is about.
{: .prompt-tip }

#### Encapsulation

Encapsulation hides the details implementation of an object and exposes only the necessary interface to the user. This enhances the data's stability and reliability and minimizes the impact of changes inside an object on the outside world.

> Consider a bank accout object.
> The balance of the account cannot be accessed directly from the outside but can only be modified through methods like 'deposit' and 'withdraw'. This method of protecting data and clearly defining how to interact with an object is the essence of encapsulation. 
{: .prompt-tip }

#### Inheritance

Inheritance allows a new class to inherit properties and methods from an existing class. This increase code reusability, reduces duplication, and enhances the system's scalability.

> If an 'Animal' class has methods like 'move' and 'eat', a 'Lion' class can inherit these methods from the 'Animal' class. Moreover, the 'Lion' can extend these functionalities by adding a new method like 'hunt'.
{: .prompt-tip }

#### Polymorphism
Polymorphism allows the same interface or method call to act in different ways. This increases the flexibility of the code and helps minimize changes.

> If there's a 'Shape' class with a method names 'draw', and classes 'Circle', 'Rectangle', and 'Triangle' inherit from 'Shape', each class can implement the 'draw' method in its own way. This allows for different outcomes for the same 'draw' method call.
{: .prompt-tip }

---

The journey of learning programming often confronts unexpected challenges. This is especially true when transitioning from procedural languages to object-oriented languages such as C++, Java, or Python, among others... This shift requires more than just learning new syntax; it necessitates a fundamental change in understanding programming.

Learning Object-Oriented Programming(OOP) can be likened to moving from mastering basic mathematics to diving into advanced algebra or calculus. This is, if you've grasped the basic elements of programming languages, OOP elevates this understanding to designing more complex and sophisticated software structures. OOP transcends mere code writing, offering strategic approaches to creating more efficient, reusable, and maintainable systems.

From this perspective, learning OOP marks a significant milestone in a developer's growth. It goes beyond the grammar and structure of programming languages, fostering a deep understanding and strategic thinking necessary to solve complex problems and materialize ideas through code.

## Conclusion

OOP offers more than just a way to write code. It provides a framework for thinking about solving complex problems and a powerful tool for modeling real-world interactions. Concepts like inheritance and polymorphism make the code more modular and flexible, showcasing their value in large-scale software development. Moreover, abstraction and encapsulation are essential for managing complexity and ensuring code stability. I view OOP not just as a programming paradigm but as a methodology for systematically addressing complex challenges.
