# Divide an Array Into Subarrays With Minimum Cost I

## Platform

LeetCode

## Problem Link

[3010. Divide an Array Into Subarrays With Minimum Cost I](https://leetcode.com/problems/divide-an-array-into-subarrays-with-minimum-cost-i/)

## Problem Statement

You are given an integer array `nums`.

You must divide the array into **three non-empty subarrays** such that:

* The first subarray contains only the first element.
* The remaining elements are split into two non-empty subarrays.
* The **cost** of a division is defined as the **sum of the first elements** of the three subarrays.

Return the **minimum possible cost** achievable by a valid division.

## Input Format

* A single integer array `nums`

  * `nums[0]` represents the first subarray
  * Elements from index `1` onward are used to form the remaining two subarrays

## Output Format

* Return a single integer representing the **minimum cost**

## Constraints

* `3 ≤ nums.length ≤ 50`
* `1 ≤ nums[i] ≤ 50`

## Examples

### Example 1

Input

```
nums = [1,2,3,12]
```

Explanation

* First subarray: `[1]`
* Remaining elements: `[2,3,12]`
* Choose the two smallest values from remaining elements → `2` and `3`

Cost calculation

```
1 + 2 + 3 = 6
```

Output

```
6
```

---

### Example 2

Input

```
nums = [5,4,3]
```

Explanation

* First subarray: `[5]`
* Remaining elements: `[4,3]`
* Only one valid split exists

Cost calculation

```
5 + 4 + 3 = 12
```

Output

```
12
```

---

### Example 3

Input

```
nums = [10,1,1,1]
```

Explanation

* First subarray: `[10]`
* Remaining elements: `[1,1,1]`
* Choose the two smallest values → `1` and `1`

Cost calculation

```
10 + 1 + 1 = 12
```

Output

```
12
```

## Approach

Greedy selection using minimum tracking.

## Intuition

The first subarray is **fixed** and always contributes `nums[0]` to the cost.

To minimize the total cost:

* The remaining two subarrays should start with the **smallest possible elements**
* This reduces the overall sum

Thus, the task reduces to finding the **two smallest values** in the subarray `nums[1 ... n-1]`.

## Algorithm Steps

* Initialize two variables to track the smallest and second smallest values.
* Traverse the array starting from index `1`.
* Update the two minimum values dynamically.
* Add `nums[0]`, smallest value, and second smallest value.
* Return the computed sum.

## Visual Walkthrough

### Case 1

```
nums = [1, 5, 3, 4]
```

Remaining elements

```
[5, 3, 4]
```

Two smallest values

```
3, 4
```

Final cost

```
1 + 3 + 4 = 8
```

---

### Case 2

```
nums = [7, 2, 9]
```

Remaining elements

```
[2, 9]
```

Final cost

```
7 + 2 + 9 = 18
```

---

### Case 3

```
nums = [6, 1, 1, 10]
```

Remaining elements

```
[1, 1, 10]
```

Final cost

```
6 + 1 + 1 = 8
```

## Complexity Analysis

### Time Complexity

**O(n)**

The array is traversed once to determine the two minimum values.

### Space Complexity

**O(1)**

Only a constant amount of extra space is used to store two minimum values.

## Solution Explanation

The solution leverages the fact that the first subarray is fixed and unavoidable.
By greedily selecting the two smallest elements from the remaining part of the array, the total cost is minimized efficiently without sorting or additional data structures.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    int minimumCost(vector<int>& nums) {

        // Array to store the two smallest values found after index 0
        int mini[2] = {50, 50};

        // Start iterating from index 1 since nums[0] is fixed
        for(int i = 1; i < nums.size(); i++) {

            // If current element is smaller than the smallest value found so far
            if(nums[i] < mini[0]) {

                // Shift the smallest value to second smallest
                mini[1] = mini[0];

                // Update the smallest value
                mini[0] = nums[i];
            }
            // If current element is between smallest and second smallest
            else if(nums[i] < mini[1]) {

                // Update second smallest value
                mini[1] = nums[i];
            }
        }

        // Total cost is the sum of:
        // - first element of nums
        // - smallest value from remaining elements
        // - second smallest value from remaining elements
        return nums[0] + mini[0] + mini[1];
    }
};
```

## Test Cases Analysis

| Input Array  | Selected Values | Output |
| ------------ | --------------- | ------ |
| `[1,2,3,12]` | `1,2,3`         | `6`    |
| `[5,4,3]`    | `5,4,3`         | `12`   |
| `[10,1,1,1]` | `10,1,1`        | `12`   |
| `[7,2,9]`    | `7,2,9`         | `18`   |

## Edge Cases to Consider

* Minimum length array of size `3`
* Duplicate minimum values
* All remaining elements equal

## Common Test Cases

* Small arrays with exactly three elements
* Arrays where the smallest values appear late
* Arrays with repeated values

## Common Mistakes to Avoid

* Including `nums[0]` when searching for minimum values
* Sorting the array unnecessarily
* Forgetting that all subarrays must be non-empty

## Interview Relevance

* Demonstrates greedy thinking
* Tests understanding of constraints-based optimization
* Common array manipulation pattern

## What This Problem Teaches

* Identifying fixed versus variable components
* Efficient minimum tracking without sorting
* Translating constraints into simple greedy logic

## Key Takeaways

* Fixed elements should be handled separately
* Greedy strategies often avoid extra overhead
* Simplicity leads to optimal performance

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on greedy intuition and efficient scanning rather than complex data structures or advanced algorithms, making it suitable for beginners and interview warm-up sessions.