---
title: Palindrome Number
date: 2024-02-04 00:40:00 +0900
categories: [CodeTest, LeetCode]
tags: [leetcode, c++]     # TAG names should always be lowercase
---

[Problem Link](https://leetcode.com/problems/palindrome-number/description/)

Given an integer `x`, return `true` if `x` is a **palindrome**, and `false` otherwise.

#### Example 1: 
* **Input**: x = 121
* **Output**: true
* **Explanation**: 121 reads as 121 from left to right and from right to left.

#### Example 2: 
* **Input**: x = -121
* **Output**: false
* **Explanation**: From left to right, its read -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

#### Example 3: 
* **Input**: 10
* **Output**: false
* **Explanation**: Reads 01 from right to left. Therefore it is not a palindrome.

#### Constraints: 
`-2³¹ <= x <= 2³¹ - 1`

**Follow up**: Could you solve it without converting the integer to string?

```c++
class Solution {
public:
    bool isPalindrome(int x) {
        // If x is negative or ends with 0 but is not 0, it cannot be a palindrome.
        if(x < 0 || (x % 10 == 0 && x != 0)) return false;

        int revercedNumber = 0;
        // Reverse half of the number to compare with the other half.
        while(x > revercedNumber) {
            // Add the last digit of x to revercedNumber.
            revercedNumber = revercedNumber * 10 + x % 10;
            x /= 10; // Remove the last digit from x.
        }

        // For numbers with an odd number of digits, we can get rid of the middle digit by reverced / 10.
        // For example, in the case of 12321, at the end of the loop we will have x = 12, revercedNumber = 123,
        // so we compare x with revercedNumber / 10.
        // This handles both even and odd length numbers by checking if the original number or its half-reversed version matches.
        return x == revercedNumber || x == revercedNumber / 10;
    }
};
```