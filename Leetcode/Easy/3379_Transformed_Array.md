# Transformed Array

## Platform

LeetCode

## Problem Link

[3379. Transformed Array](https://leetcode.com/problems/transformed-array/)

## Problem Statement

You are given an integer array `nums` of length `n`.

You need to construct a new array `res` of the same length such that for every index `i`:

* The value at `res[i]` is taken from `nums` at a position determined by shifting index `i` by `nums[i]` positions.
* The array is treated as **circular**, meaning indices wrap around using modulo arithmetic.
* Negative shifts are allowed and must also wrap correctly.

Formally:

```
res[i] = nums[(i + nums[i]) mod n]
```

Return the transformed array `res`.

## Input Format

* A single integer array `nums`

## Output Format

* Return an integer array `res` representing the transformed array

## Constraints

* `1 ≤ nums.length ≤ 10^5`
* `-10^9 ≤ nums[i] ≤ 10^9`

## Examples

### Example 1

Input

```
nums = [1, 2, 3, 4]
```

Explanation

Index-wise transformation:

* `i = 0` → `(0 + 1) % 4 = 1` → `nums[1] = 2`
* `i = 1` → `(1 + 2) % 4 = 3` → `nums[3] = 4`
* `i = 2` → `(2 + 3) % 4 = 1` → `nums[1] = 2`
* `i = 3` → `(3 + 4) % 4 = 3` → `nums[3] = 4`

Output

```
[2, 4, 2, 4]
```

### Example 2

Input

```
nums = [-1, -2, -3]
```

Explanation

* `i = 0` → `(0 - 1) % 3 = -1 → wrapped to 2` → `nums[2] = -3`
* `i = 1` → `(1 - 2) % 3 = -1 → wrapped to 2` → `nums[2] = -3`
* `i = 2` → `(2 - 3) % 3 = -1 → wrapped to 2` → `nums[2] = -3`

Output

```
[-3, -3, -3]
```

## Approach

**Direct index transformation using modular arithmetic**

## Intuition

Each element in the result array depends only on:

* Its current index `i`
* The value `nums[i]`
* The array length `n`

Since the array is circular:

* Index shifts must wrap around
* Negative indices must be normalized into the valid range `[0, n-1]`

A carefully written modulo expression ensures correctness for both positive and negative shifts.

## Algorithm Steps

* Let `n` be the length of `nums`
* Initialize a result array `res` of size `n`
* For each index `i` from `0` to `n-1`:

  * Compute shifted index

    ```
    idx = ((i + nums[i]) % n + n) % n
    ```
  * Set `res[i] = nums[idx]`
* Return `res`

## Visual Walkthrough

### Test Case 1

Input:

```
nums = [2, -1, 1]
```

Step-by-step:

* `i = 0` → `0 + 2 = 2` → `nums[2] = 1`
* `i = 1` → `1 - 1 = 0` → `nums[0] = 2`
* `i = 2` → `2 + 1 = 3 → 3 % 3 = 0` → `nums[0] = 2`

Output:

```
[1, 2, 2]
```

---

### Test Case 2

Input:

```
nums = [0, 0, 0]
```

Each index maps to itself.

Output:

```
[0, 0, 0]
```

---

### Test Case 3

Input:

```
nums = [5]
```

Single-element array:

```
(0 + 5) % 1 = 0
```

Output:

```
[5]
```

## Complexity Analysis

### Time Complexity

**O(n)**

Each element is processed exactly once using constant-time operations.

### Space Complexity

**O(n)**

A new array of size `n` is created to store the result.

## Solution Explanation

The solution constructs the transformed array by applying a circular index shift for each position.
To handle negative values safely, the index calculation normalizes the result using a double modulo pattern:

```
((i + nums[i]) % n + n) % n
```

This guarantees that the computed index always lies within valid bounds, regardless of the sign or magnitude of `nums[i]`.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    vector<int> constructTransformedArray(vector<int>& nums) {

        int n = nums.size();

        // Result array of the same size
        vector<int> res(n);

        // Process each index
        for (int i = 0; i < n; i++) {

            // Compute the circular index safely
            int idx = ((i + nums[i]) % n + n) % n;

            // Assign the transformed value
            res[i] = nums[idx];
        }

        return res;
    }
};
```

## Test Cases Analysis

| Test Case | Input      | Computed Indices | Output     |
| --------- | ---------- | ---------------- | ---------- |
| 1         | [1,2,3,4]  | 1,3,1,3          | [2,4,2,4]  |
| 2         | [-1,-2,-3] | 2,2,2            | [-3,-3,-3] |
| 3         | [0,0,0]    | 0,1,2            | [0,0,0]    |
| 4         | [5]        | 0                | [5]        |

## Edge Cases to Consider

* Very large positive shifts
* Very large negative shifts
* Single-element arrays
* All zero values

## Common Test Cases

* Mixed positive and negative values
* Large array sizes
* Repeated values

## Common Mistakes to Avoid

* Using modulo without handling negative values
* Forgetting that the array is circular
* Accessing indices outside the valid range

## Interview Relevance

* Tests understanding of modulo arithmetic
* Evaluates array indexing discipline
* Common pattern in circular array problems

## What This Problem Teaches

* Safe modulo handling in programming
* Circular data structure traversal
* Mapping indices through transformations

## Key Takeaways

* Modulo with negatives must be handled carefully
* Direct formulas can replace simulation
* Clean math simplifies array problems

## Problem Difficulty Analysis

This is an **Easy-to-Medium** level problem.
While the logic is straightforward, correct handling of circular indexing and negative values is essential for correctness.