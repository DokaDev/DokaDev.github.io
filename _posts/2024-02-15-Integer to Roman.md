---
title: Integer to Roman
date: 2024-02-15 14:10:00 +0900
categories: [CodeTest, LeetCode]
math: true
tags: [leetcode, c++]     # TAG names should always be lowercase
---

[Problem Link](https://leetcode.com/problems/integer-to-roman/submissions/1175729995/)

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

| Symbol | Value |
| ------ | ----- |
| I      | 1     |
| V      | 5     |
| X      | 10    |
| L      | 50    |
| C      | 100   |
| D      | 500   |
| M      | 1000  |

For example, `2` is written as `II` in Roman numeral, just two one's added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used.

* `I` can be placed before `V`(5) and `X`(10) to make 4 and 9.
* `X` can be placed before `L`(50) and `C`(100) to make 40 and 90.
* `C` can be placed before `D`(500) and `M`(1000) to make 400 and 900.

Given an integer, convert it to a roman numeral.



#### Example 1:

* **Input**: num = 3
* **Output**: "III"
* **Explanation**: 3 is represented as 3 ones.



#### Example 2:

* **Input**: num = 58
* **Output**: "LVIII"
* **Explanation**: L = 50, V = 5, III = 3



#### Example 3:

* **Input**: num = 1994
* **Output**: "MCMXCIV"
* **Explanation**: M = 1000, CM = 900, XC = 90 and IV = 4.



#### Constraints:

* $1 \le num \le 3999$



---

#### Solution

* **Objective**: Convert integers to Roman numerals.
* **Roman Numeral Symbols**:  I(1), V(5), X(10), L(50), C(100), D(500), M(1000)



##### Conversion Rules

* Mostly written in descending order from larger to smaller values.
* Specific combinations where a smaller value precedes a larger value imply subtraction(e.g., IV = 4, IX = 9)



##### Implementation Method

* **Value and Symbol Mapping**: Store the numbers and corresponding Roman numeral symbols in arrays.
* **Conversion Process**: 
  * Start with the given integer.
  * If the integer is greater than or equal to the current Roman numeral value, append the symbol to the result and subtract the value.
  * Repeat for all Roman numeral values.

```c++
class Solution {
public:
    string intToRoman(int num) {
        // Arrays to store the values corresponding to Roman numerals
        vector<int> values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        vector<string> symbols = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};

        // String to store the resulting Roman numeral
        string roman = "";

        // Convert the given number to a Roman numeral
        for(int i = 0; i < values.size() && num > 0; i++) {
            // Check how many times the current value can represent the number
            while(num >= values[i]) { 
                num -= values[i];   // Substract the value from num
                roman += symbols[i];    // Add the corresponding Roman Numeral to the result
            }
            return roman;
        }
    }
}
```