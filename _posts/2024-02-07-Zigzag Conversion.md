---
title: Zigzag Conversion
date: 2024-02-04 00:01:00 +0900
categories: [CodeTest, LeetCode]
tags: [leetcode, c++]     # TAG names should always be lowercase
---

[Problem Link](https://leetcode.com/problems/zigzag-conversion)

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

> P   A   H   N
> A P L S I I G
> Y   I   R

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:
```c++
string convert(string s, int numRows);
```

#### Example 1:
* **Input**: s = "PAYPALISHIRING", numRows = 3
* **Output**: "PAHNAPLSIIGYIR"

#### Example 2:
* **Input**: s = "PAYPALISHIRING", numRows = 4
* **Output**: "PINALSIGYAHRPI"
* **Explanation**:
    P     I    N
    A   L S  I G
    Y A   H R
    P     I

#### Example 3:
* **Input**: s = "A", numRows = 1
* **Output**: "A"

#### Constrains:
* `1 <= s.length <= 1000`
* `s` consists of English letters (lower-case and upper-case), `,`, `','` and `'.'`.
* `1 <= numRows <= 1000`

```c++
#include <vector>
#include <string>

using namespace std;

class Solution {
public:
    string convert(string s, int numRows) {
        // If numRows is 1 or less than or equal to the length of s, return s as is
        if (numRows == 1 || numRows >= s.length()) {
            return s;
        }

        // Initialize an array of strings to store characters for each row
        vector<string> rows(min(numRows, int(s.length())));
        int curRow = 0;
        bool goingDown = false;

        // Iterate through each character in the string and append it to the appropriate row
        for (char c : s) {
            rows[curRow] += c;
            // Change direction when reaching the first or the last row
            if (curRow == 0 || curRow == numRows - 1) goingDown = !goingDown;
            curRow += goingDown ? 1 : -1;
        }

        // Combine characters from all rows into a single string
        string ret;
        for (string row : rows) ret += row;

        return ret;
    }
};
```