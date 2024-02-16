---
title: Euclidean Algorithm
date: 2024-02-16 15:50:00 +0900
image: 
    path: /assets/post/cs/algorithm/0.png
    alt: The cover image is created by DALL-E
categories: [Computer Science, Algorithm]
math: true
tags: [algorithm]     # TAG names should always be lowercase
---

Euclidean algorithm, introduced by the ancient Greek mathematician Euclid in "Elements," continues to hold significant value today. This simple yet powerful algorithm provides a fundamental and efficient method for finding the **Greatest Common Divisor(GCD)** of two natural numbers. This article will explore the concept of the Euclidean algorithm, its principles, implementation using C++, and how this algorithm can be applied to solve real-world problems.

## Concept of the Euclidean Algorithm

The Euclidean algorithm calculates the GCD of two natural numbers, $A$ and $B(A > B)$, based on the principle that the GCD of $A$ and $B$ is the same as the GCD of $B$ and the remainder `R` of $A$ divided by $B$. This process is repeated until the remainder `R` becomes 0, at which point $B$ is the GCD of $A$ and $B$.

### Detailed Explanation of the Algorithm Principle

The Euclidean algorithm simplifies the process of finding the GCD of two natural numbers $A$ and $B$. The mathematical principle of the Euclidean algorithm can be expressed as follows:
$$
GCD(A, B) = GCD(B, A\mod B)
$$


Here, $A \mod B$ represents the remainder  of $A$ divided by $B$. This formula indicates that the GCD of $A$ and $B$ is identical to the GCD of $B$ and $A \mod B$.

The process can be detailed as follows:

1. **Input**: Two natural numbers $A$ and $B$ are received as input. If $A < B$, the positions of the two numbers are swapped within the algorithm to ensure that $A$ is greater than $B$, providing flexibility and generalizing the starting condition.
2. **Calculate Remainder**: Calculate the remainder `R` of $A$ divided by $B$. This step is key to transforming the relationship between $A$ and $B$ into a smaller numerical relationship.
3. **Swap Values**: Set the value of $B$ to $A$, and the calculated remainder `R` to $B$. This process gradually reduces the problem size, preparing for the final derivation of the GCD.
4. **Repeat**: Repeat steps 2 and 3 until $B$ becomes 0. At the moment $B$ is 0, the values stored in $A$ is the GCD of the two numbers $A$ and $B$.

This method allows for the efficient determination of the GCD of any two natural number, demonstrating the powerful mathematical principle within the simplicity of the Euclidean algorithm.



## Implementation Using C++

> This code calculates and outputs the GCD of two integer entered by the user using the Euclidean algorithm.
{: .prompt-info  }

```c++
#include <iostream>

// Function to find the Greatest Common Divisor(GCD) of two numbers using the Euclidean algorithm
int gcd(int a, int b) {
    if (a < b) {
        // If a is smaller than b, swap the values of a and b
        int temp = a;
        a = b;
        b = temp;
    }
    while(b != 0) { // Repeat until b is not 0
        int r = a % b; // Store the remainder of a divided by b in r
        a = b; // Set the value of b to a
        b = r; // Set the value of the remainder r to b
    }
    return a; // When b is 0, the current value of a is the GCD
}

int main() {
    int num1, num2;
    std::cout << "Enter two integers: ";
    std::cin >> num1 >> num2;

    std::cout << "The GCD of " << num1 << " and " << num2 << " is " << gcd(num1, num2) << std::endl;

    return 0;
}
```

Reflecting on the Euclidean algorithm has deepened my appreciation for its enduring value and significance in modern computer science. The fact that this method, discovered thousands of years ago, still plays a crucial role in solving various problems today emphasizes the timeless value of a good algorithm.

The Euclidean algorithm, while simple, contains deep mathematical insight that transcend its aesthetic beauty and are vitally important in practical terms. It encourages us to think more deeply about how we solve problems, highlighting the importance of simplifying complex issues. Through the Euclidean algorithm, we learn how fundamental principle can be powerfully effective in solving difficult problems.
