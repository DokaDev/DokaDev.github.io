---
title: Tower of Hanoi
date: 2024-02-19 23:20:00 +0900
categories: [Computer Science, Algorithm]
math: true
tags: [algorithm]     # TAG names should always be lowercase
---

The Tower of Hanoi transcends a mere puzzle game to become a textbook example in computer science for understanding recursive thinking. The goal of this game is to move all the disks from the first to the third pillar using several disks a different sizes. During this process, only one disk can be moved at a time, and a larger disk cannot be placed on top of a smaller disk.



## The Principle and Solution of the Algorithm

The algorithm to solve the Tower of Hanoi problems is based on the recursive call applying the divide and conquer strategy. The core idea of solving this problem recursively is to move all the disks except the largest one to the auxiliary pillar before moving the largest disk to the destination pillar, and then move the rest of the disks on top of the largest disk to the destination pillar. This process is completed in a minimum on $2^n - 1$ moves when there are n disks.



### Application cases of the Tower of Hanoi

The Tower of Hanoi algorithm is frequently used in computer science education to teach recursive thinking and algorithm design. Additionally, this algorithm aids in understanding various concepts in computer programs, such as stack calls and memory management. Beyond educational purposes, this puzzle is also used as a tool to test or improve programming skills.



### Implementing the Tower of Hanoi in C++

> The following code demonstrates the process of solving the Tower of Hanoi problem with 3 disks. This code effectively solves the problem using a recursive function, with each move printed out to allow users to easily follow the process of moving the disks.
{: .prompt-info }

```cpp
#include <iostream>
using namespace std;

void towerOfHanoi(int n, char from_rod, char to_rod, char aux_rod) {
    if(n == 0) return; // base case
    
    towerOfHanoi(n - 1, from_rod, aux_rod, to_rod); // Move n-1 disks to the auxiliary rod
    cout << "Move disk " << n << " from rod " << from_rod << " to rod " << to_rod << endl; // Move the largest disk
    towerOfHanoi(n - 1, aux_rod, to_rod, from_rod); // Move the n-1 disks from the auxiliary rod to the destination rod
}
```



Indeed, the process of solving the Tower of Hanoi problems can serve as an excellent metaphor for how we can systematically decompose and solve complex problems we face. This approach helps us to employ flexibility and creativity in overcoming the various challenges we encounter in life.
