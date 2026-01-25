# 1984. Minimum Difference Between Highest and Lowest of K Scores

## Platform

LeetCode

## Problem Link

[1984. Minimum Difference Between Highest and Lowest of K Scores](https://leetcode.com/problems/minimum-difference-between-highest-and-lowest-of-k-scores/)

## Problem Statement

You are given an integer array `nums`, where each element represents a score, and an integer `k`.

You must select **exactly `k` scores** such that the **difference between the highest and lowest selected scores** is minimized.

Return the **minimum possible difference**.

## Input Format

* An integer array `nums`
* An integer `k`, the number of scores to select

## Output Format

Return a single integer representing the minimum possible difference between the highest and lowest of the selected `k` scores.

## Constraints

* `1 ≤ k ≤ nums.length ≤ 1000`
* `0 ≤ nums[i] ≤ 10^5`

## Examples

### Example 1

Input

```
nums = [90]
k = 1
```

Explanation

Only one score is selected, so the difference is `0`.

Output

```
0
```

### Example 2

Input

```
nums = [9,4,1,7]
k = 2
```

Explanation

After sorting:

```
[1, 4, 7, 9]
```

Possible selections:

* (1, 4) → difference = 3
* (4, 7) → difference = 3
* (7, 9) → difference = 2

Minimum difference is `2`.

Output

```
2
```

## Approach

Sorting with Sliding Window technique.

## Intuition

If the array is sorted, any group of `k` elements that minimizes the difference must be **contiguous**.

Instead of checking all combinations, which would be inefficient, we slide a window of size `k` across the sorted array and compute the difference between the first and last elements of each window.

The smallest such difference is the answer.

## Algorithm Steps

* Sort the array `nums`.
* Initialize two pointers:

  * `left` at index `0`
  * `right` at index `k - 1`
* Initialize a variable to store the minimum difference.
* While `right` is within array bounds:

  * Compute `nums[right] - nums[left]`
  * Update the minimum difference
  * Increment both `left` and `right`
* Return the minimum difference found.

## Visual Walkthrough

### Test Case 1

Input:

```
nums = [9,4,1,7], k = 2
```

Sorted array:

```
[1, 4, 7, 9]
```

Sliding window comparisons:

```
[1, 4] → diff = 3
[4, 7] → diff = 3
[7, 9] → diff = 2
```

Minimum difference:

```
2
```

---

### Test Case 2

Input:

```
nums = [1, 3, 6, 10, 15], k = 3
```

Sorted array:

```
[1, 3, 6, 10, 15]
```

Windows:

```
[1, 3, 6] → diff = 5
[3, 6, 10] → diff = 7
[6, 10, 15] → diff = 9
```

Minimum difference:

```
5
```

## Complexity Analysis

### Time Complexity

O(n log n)

The array is sorted once, which dominates the runtime.
The sliding window traversal is linear.

### Space Complexity

O(1)

Sorting is done in-place, and only constant extra variables are used.

## Solution Explanation

The solution leverages sorting to simplify the problem.
Once sorted, the smallest difference between the highest and lowest values among any `k` elements will always occur within a contiguous segment.

By sliding a fixed-size window and tracking the minimum difference, the algorithm efficiently finds the optimal answer.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    int minimumDifference(vector<int>& nums, int k) {

        // Get the size of the array
        int n = nums.size();

        // Sort the array to enable sliding window comparison
        sort(nums.begin(), nums.end());

        // Initialize the minimum difference to a very large value
        int mini = INT_MAX;

        // Left and right pointers for the sliding window
        int left = 0;
        int right = k - 1;

        // Slide the window while it stays within bounds
        while (right < n) {

            // Update the minimum difference for the current window
            mini = min(mini, nums[right] - nums[left]);

            // Move the window forward
            left++;
            right++;
        }

        // Return the smallest difference found
        return mini;
    }
};
```

## Test Cases Analysis

| nums          | k | Output | Explanation        |
| ------------- | - | ------ | ------------------ |
| [90]          | 1 | 0      | Single element     |
| [9,4,1,7]     | 2 | 2      | Best adjacent pair |
| [1,3,6,10,15] | 3 | 5      | Smallest window    |
| [1,1,1,1]     | 2 | 0      | All equal          |

## Edge Cases to Consider

* `k = 1` (difference is always `0`)
* All elements equal
* Large input sizes

## Common Test Cases

* Small arrays
* Arrays requiring sorting
* Arrays with duplicate values

## Common Mistakes to Avoid

* Forgetting to sort the array
* Using brute-force combinations
* Incorrect window boundaries

## Interview Relevance

* Demonstrates sliding window optimization
* Tests understanding of sorting-based strategies
* Common array optimization problem

## What This Problem Teaches

* Transforming problems using sorting
* Efficient window-based comparisons
* Reducing brute-force complexity

## Key Takeaways

* Sorting can simplify selection problems
* Sliding windows provide optimal performance
* Always analyze constraints before choosing an approach

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on optimization techniques and efficient traversal rather than complex logic.