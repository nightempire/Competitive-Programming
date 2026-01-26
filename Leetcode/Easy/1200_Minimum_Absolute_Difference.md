# 1200. Minimum Absolute Difference

## Platform

LeetCode

## Problem Link

[1200. Minimum Absolute Difference](https://leetcode.com/problems/minimum-absolute-difference/)

## Problem Statement

You are given an array of **distinct integers** `arr`.

Your task is to find all pairs of elements with the **minimum absolute difference** between any two elements in the array.

Return a list of pairs `[a, b]` in **ascending order**, where `a < b` and `|a - b|` equals the minimum absolute difference found.

## Input Format

* An integer array `arr` containing distinct integers

## Output Format

Return a 2D array containing all pairs of integers with the minimum absolute difference.

Each pair must be in ascending order, and the list of pairs must also be sorted in ascending order.

## Constraints

* `2 ≤ arr.length ≤ 10^5`
* `-10^6 ≤ arr[i] ≤ 10^6`
* All elements in `arr` are distinct

## Examples

### Example 1

Input

```
arr = [4,2,1,3]
```

Explanation

After sorting:

```
[1, 2, 3, 4]
```

Absolute differences:

```
2 - 1 = 1
3 - 2 = 1
4 - 3 = 1
```

Minimum difference is `1`.

Output

```
[[1,2],[2,3],[3,4]]
```

### Example 2

Input

```
arr = [1,3,6,10,15]
```

Explanation

Sorted array:

```
[1, 3, 6, 10, 15]
```

Differences:

```
3 - 1 = 2
6 - 3 = 3
10 - 6 = 4
15 - 10 = 5
```

Minimum difference is `2`.

Output

```
[[1,3]]
```

## Approach

Sorting followed by adjacent difference comparison.

## Intuition

The smallest absolute difference between any two elements in an array will always occur between **adjacent elements in the sorted array**.

Instead of checking all possible pairs, which would be inefficient, sorting allows us to reduce the problem to a linear scan.

## Algorithm Steps

* Sort the array `arr`.
* Initialize a variable `mini` to store the minimum absolute difference.
* Traverse the sorted array to compute differences between adjacent elements and update `mini`.
* Traverse the array again:

  * If the difference between adjacent elements equals `mini`, add the pair to the result list.
* Return the result list.

## Visual Walkthrough

### Test Case 1

Input:

```
[4, 2, 1, 3]
```

Sorted:

```
[1, 2, 3, 4]
```

Differences:

```
1, 1, 1
```

Pairs with minimum difference:

```
(1,2), (2,3), (3,4)
```

---

### Test Case 2

Input:

```
[8, 1, 5, 12]
```

Sorted:

```
[1, 5, 8, 12]
```

Differences:

```
4, 3, 4
```

Minimum difference:

```
3
```

Pair:

```
(5,8)
```

## Complexity Analysis

### Time Complexity

O(n log n)

Sorting dominates the runtime.
The two linear traversals are O(n).

### Space Complexity

O(1) (excluding output)

The algorithm uses constant extra space apart from the result list.

## Solution Explanation

By sorting the array, the solution ensures that the smallest absolute differences can be found by examining only adjacent elements.

The first pass determines the minimum difference, and the second pass collects all pairs matching that difference.
This method is efficient, clean, and directly aligned with the problem constraints.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    vector<vector<int>> minimumAbsDifference(vector<int>& arr) {

        // Result container for pairs with minimum absolute difference
        vector<vector<int>> res;

        // Sort the array to compare adjacent elements
        sort(arr.begin(), arr.end());

        // Number of elements
        int n = arr.size();

        // Initialize minimum difference to a large value
        int mini = INT_MAX;

        // First pass: find the minimum absolute difference
        for (int i = 1; i < n; i++) {
            mini = min(mini, arr[i] - arr[i - 1]);
        }

        // Second pass: collect all pairs with the minimum difference
        for (int i = 1; i < n; i++) {
            if (arr[i] - arr[i - 1] == mini) {
                res.push_back({arr[i - 1], arr[i]});
            }
        }

        // Return the result
        return res;
    }
};
```

## Test Cases Analysis

| Input Array   | Output              | Explanation              |
| ------------- | ------------------- | ------------------------ |
| [4,2,1,3]     | [[1,2],[2,3],[3,4]] | All adjacent diffs equal |
| [1,3,6,10,15] | [[1,3]]             | Minimum diff is 2        |
| [3,8,15]      | [[8,15]]            | Only one minimum pair    |
| [1,100]       | [[1,100]]           | Single possible pair     |

## Edge Cases to Consider

* Array of size 2
* Large integer values
* Negative numbers

## Common Test Cases

* Already sorted arrays
* Reverse sorted arrays
* Arrays with evenly spaced values

## Common Mistakes to Avoid

* Checking all possible pairs unnecessarily
* Forgetting to sort the array
* Missing multiple valid pairs

## Interview Relevance

* Tests understanding of sorting-based optimization
* Evaluates ability to reduce brute-force approaches
* Common array-processing interview problem

## What This Problem Teaches

* Leveraging sorted order for efficiency
* Two-pass scanning techniques
* Careful handling of result collection

## Key Takeaways

* Sorting simplifies difference-based problems
* Adjacent comparisons are often sufficient
* Clean logic improves both performance and readability

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on recognizing patterns after sorting and implementing an efficient linear scan solution.