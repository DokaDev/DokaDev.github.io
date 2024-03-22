---
title: 3Sum Closest 
date: 2024-02-21 17:00:00 +0900
math: true
categories: [CodeTest, LeetCode]
tags: [leetcode, c++]     # TAG names should always be lowercase
---

[Problem Link](https://leetcode.com/problems/3sum-closest)

Given an integer array `nums` of length `n` and an integer `target`, find three integers in `nums` such that the sum is closest to `target`.

Return *the sum of the three integers*.

You may assume that each input would have exactly one solution.



#### Example 1:

* **Input**: nums = [-1, 2, 1, -4], target = 1
* **Output**: 2
* **Explanation**: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2)



#### Example 2:

* **Input**: nums = [0, 0, 0], target = 1
* **Output**: 0
* **Explanation**: The sum that is closest to the target is 0. (0 + 0 + 0 = 0)



#### Constraints:

* $3 \le nums.length \le 500$
* $-1000 \le nums[i] \le 1000$
* $-10^4 \le target \le 10^4$

---

#### Solution

The algorithm used to solve this problem is **Sorting and Two Pointer Approach**. First, the given array is sorted in acending order, and then for each element, the rest of the array is searched using two pointers to find the sum closest to the target.



##### Solution Ideas

1. **Sort the array**: The input array needs to be sorted in ascending order to apply the two-pointer approach effectively.
2. **Two Pointer Approach**: For each element in the array, fix it and use two pointers at the start and end of the remaining array. Move these pointers to find the sum of three numbers that is closest to the target.
3. **Update the Closest Difference**: During the iteration, if the difference between the target and the sum of three numbers is less than the previously found minimum difference, update the sum of the three numbers.



##### Implement

1. **Array Sorting**

   ```c++
   sort(nums.begin(), nums.end());
   ```

2. **Setting and Searching with Two Pointers**:

   ```c++
   for(int i = 0; i < nums.size(); i++) {
       int left = i + 1, right = nums.size() - 1;
       
       while(left < right) {
           int sum = nums[i] + nums[left] + nums[right];
           if(abs(target - sum) < abs(target - closest)) closest = sum;
           
           if(sum > target) right--;
           else if(sum < target) left++;
           else return sum;
       }
   }
   ```

3. **Updating the Closest Difference**:

   This logic is implemented within the code block above. The condition `abs(target - sum) < abs(target - closest)` is used to update the closest difference.

   Through this process, it's possible to efficiently find the sum of three sumbers from the given array `nums` that is closest to `target`.

```c++
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end()); // Sort the array in ascending order
        int closestSum = nums[0] + nums[1] + nums[2]; // Initialize the closest sum (with the sum of the first three elements)

        // Traverse the array for each element
        for(int i = 0; i < nums.size() - 2; i++) {
            int left = i + 1, right = nums.size() - 1;

            while(left < right) {
                // Calculate the current sum of three elements
                int currentSum = nums[i] + nums[left] + nums[right];
                
                // If the difference between the current sum and the target is smaller than the previously found closest sum, update it
                if(abs(target - currentSum) < abs(target - closestSum)) closestSum = currentSum; 

                if(currentSum > target) right--;
                else if(currentSum < target) left++;
                else return currentSum; // If the current sum exactly matches the target, return the current sum immediately
            }
        }
        return closestSum; // Return the closest sum after checking all combinations
    }
};
```

