# 1877. Minimize Maximum Pair Sum in Array

## Platform

LeetCode

## Problem Link

[1877. Minimize Maximum Pair Sum in Array](https://leetcode.com/problems/minimize-maximum-pair-sum-in-array/)

## Problem Statement

You are given an integer array `nums` of even length.

In one operation, you can form pairs of elements such that **each element is used exactly once**.
For every formed pair, compute the **sum of the two elements**.

Your objective is to **minimize the maximum pair sum** among all pairs by choosing an optimal pairing strategy.

Return the minimized value of the maximum pair sum.

## Input Format

* An integer array `nums`
* The length of `nums` is even

## Output Format

* Return a single integer — the minimum possible value of the maximum pair sum

## Constraints

* `2 ≤ nums.length ≤ 10^5`
* `nums.length` is even
* `1 ≤ nums[i] ≤ 10^5`

## Examples

### Example 1

Input

```
nums = [3,5,2,3]
```

Explanation

After sorting:

```
[2,3,3,5]
```

Possible optimal pairing:

```
(2,5) → sum = 7
(3,3) → sum = 6
```

Maximum pair sum = `7`

Output

```
7
```

---

### Example 2

Input

```
nums = [3,5,4,2,4,6]
```

Explanation

After sorting:

```
[2,3,4,4,5,6]
```

Optimal pairing:

```
(2,6) → 8
(3,5) → 8
(4,4) → 8
```

Maximum pair sum = `8`

Output

```
8
```

---

### Example 3

Input

```
nums = [1,1,1,1]
```

Explanation

All pairs:

```
(1,1) → 2
(1,1) → 2
```

Maximum pair sum = `2`

Output

```
2
```

## Approach

**Greedy Strategy with Sorting and Two Pointers**

## Intuition

To minimize the **maximum** pair sum:

* Pair the **smallest element** with the **largest element**
* This balances extreme values and prevents large numbers from forming excessively large sums

Any other pairing strategy would either:

* Increase the maximum sum, or
* Fail to distribute large values evenly

This is a classic greedy pairing problem.

## Algorithm Steps

* Sort the array `nums` in non-decreasing order.
* Initialize two pointers:

  * `left` at the beginning of the array
  * `right` at the end of the array
* Initialize a variable `maxi` to store the maximum pair sum.
* While `left < right`:

  * Compute `nums[left] + nums[right]`
  * Update `maxi` with the maximum of its current value and this sum
  * Move `left` forward and `right` backward
* Return `maxi`.

## Visual Walkthrough

### Test Case 1

Input

```
[3,5,2,3]
```

Sorted:

```
[2,3,3,5]
```

Pairing process:

```
left=2, right=5 → sum=7 → maxi=7
left=3, right=3 → sum=6 → maxi=7
```

Final answer:

```
7
```

---

### Test Case 2

Input

```
[2,3,4,4,5,6]
```

Pairing:

```
(2,6)=8
(3,5)=8
(4,4)=8
```

All sums equal → answer = `8`

## Complexity Analysis

### Time Complexity

**O(n log n)**

* Sorting the array takes `O(n log n)`
* Two-pointer traversal takes `O(n)`

Overall complexity is dominated by sorting.

### Space Complexity

**O(1) auxiliary space**

* Sorting is done in place
* Only constant extra variables are used

## Solution Explanation

The solution sorts the array and pairs elements symmetrically from the ends.
This ensures that large values are always balanced by small values, preventing any single pair from dominating the maximum sum.

By tracking the largest pair sum during this process, the algorithm efficiently computes the optimal answer.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    int minPairSum(vector<int>& nums) {

        // Sort the array to enable optimal pairing
        sort(nums.begin(), nums.end());

        // Two pointers for smallest and largest elements
        int left = 0;
        int right = nums.size() - 1;

        // Variable to store the maximum pair sum
        int maxi = 0;

        // Pair elements from both ends
        while (left < right) {

            // Update maximum pair sum
            maxi = max(maxi, nums[left] + nums[right]);

            // Move pointers inward
            left++;
            right--;
        }

        // Return the minimized maximum pair sum
        return maxi;
    }
};
```

## Test Cases Analysis

| Test Case | Input Array          | Pair Sums       | Output |
| --------- | -------------------- | --------------- | ------ |
| 1         | [3,5,2,3]            | 7, 6            | 7      |
| 2         | [3,5,4,2,4,6]        | 8, 8, 8         | 8      |
| 3         | [1,1,1,1]            | 2, 2            | 2      |
| 4         | [1,2,3,4]            | 5, 5            | 5      |
| 5         | Large balanced array | Uniform max sum | Valid  |

## Edge Cases to Consider

* All elements equal
* Array with only two elements
* Very large values near constraints
* Already sorted or reverse-sorted arrays

## Common Test Cases

* Mixed small and large numbers
* Symmetric distributions
* Random unsorted arrays

## Common Mistakes to Avoid

* Pairing adjacent elements instead of extreme values
* Forgetting to sort before pairing
* Tracking the minimum instead of the maximum pair sum

## Interview Relevance

* Demonstrates greedy optimization
* Tests understanding of two-pointer techniques
* Common problem pattern in array pairing questions

## What This Problem Teaches

* How greedy strategies can minimize worst-case outcomes
* Effective use of sorting to simplify pairing logic
* Importance of balancing extremes in optimization problems

## Key Takeaways

* Pair smallest with largest to minimize the maximum sum
* Sorting often enables optimal greedy solutions
* Two-pointer techniques are powerful for symmetric pairing problems

## Problem Difficulty Analysis

This is a **Medium-level** problem.
While the implementation is straightforward, identifying the correct greedy strategy is the key challenge, making it a frequent interview question for array optimization scenarios.
