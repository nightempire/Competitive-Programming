# Construct the Minimum Bitwise Array I

## Platform

LeetCode

## Problem Link

[3314. Construct the Minimum Bitwise Array I](https://leetcode.com/problems/construct-the-minimum-bitwise-array-i/)

## Problem Statement

You are given an integer array `nums`.

For each element `nums[i]`, you must determine the **minimum non-negative integer `x`** such that:

```
x | (x + 1) = nums[i]
```

If no such integer exists, return `-1` for that position.

The final result should be an array where each index contains the computed value for the corresponding element in `nums`.

## Input Format

* An integer array `nums`

## Output Format

* An integer array `res` of the same length as `nums`
* For each index:

  * `res[i]` is the smallest integer `x` such that `x | (x + 1) = nums[i]`
  * `-1` if no such integer exists

## Constraints

* `1 ≤ nums.length ≤ 100`
* `1 ≤ nums[i] ≤ 10^9`

## Examples

### Example 1

Input

```
nums = [3, 7, 5]
```

Explanation

* For `3`:

  * `1 | 2 = 3` → valid, minimum
* For `7`:

  * `3 | 4 = 7` → valid
* For `5`:

  * No integer `x` satisfies `x | (x + 1) = 5`

Output

```
[1, 3, -1]
```

### Example 2

Input

```
nums = [1, 2]
```

Explanation

* `1`: no valid `x`
* `2`: no valid `x`

Output

```
[-1, -1]
```

## Approach

**Brute-Force Bitwise Search**

## Intuition

The bitwise OR operation combines all set bits from both operands.

By testing increasing values of `x` starting from `1`, we can directly check whether:

```
x | (x + 1)
```

matches the given number.

Because the problem requires the **minimum possible `x`**, the first valid match can be returned immediately.

If no value satisfies the condition, the answer is `-1`.

## Algorithm Steps

* Initialize an empty result array
* For each value `num` in `nums`:

  * Set a flag to track whether a valid `x` is found
  * Iterate `x` from `1` to `num - 1`
  * If `(x | (x + 1)) == num`:

    * Store `x` in the result array
    * Mark the flag as true
    * Stop further searching for this number
  * If no valid `x` is found:

    * Store `-1`
* Return the result array

## Visual Walkthrough

### Case 1: `num = 3`

Check values:

```
1 | 2 = 3  → match found
```

Result:

```
1
```

---

### Case 2: `num = 7`

Check values:

```
1 | 2 = 3
2 | 3 = 3
3 | 4 = 7  → match found
```

Result:

```
3
```

---

### Case 3: `num = 5`

Check values:

```
1 | 2 = 3
2 | 3 = 3
3 | 4 = 7
4 | 5 = 5? → false
```

Result:

```
-1
```

## Complexity Analysis

### Time Complexity

**O(n × m)**

* `n` = length of `nums`
* `m` = value of `nums[i]` in the worst case

Each number may require checking all integers from `1` to `nums[i] - 1`.

### Space Complexity

**O(n)**

The result array stores one integer per input element.

## Solution Explanation

The solution evaluates each element independently.
By iterating from the smallest possible candidate upward and checking the bitwise OR condition, the algorithm guarantees that the first valid match is the minimum one.
The logic is straightforward and closely follows the problem definition.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    vector<int> minBitwiseArray(vector<int>& nums) {

        // Result array to store answers for each element
        vector<int> res;

        // Reserve space to improve performance
        res.reserve(nums.size());

        // Process each number independently
        for (int num : nums) {

            // Flag to track whether a valid x is found
            bool found = false;

            // Try all possible x values from 1 to num - 1
            for (int x = 1; x < num; x++) {

                // Check if bitwise OR of x and x+1 equals num
                if ((x | (x + 1)) == num) {

                    // Store the minimum valid x
                    res.push_back(x);

                    // Mark as found and stop searching
                    found = true;
                    break;
                }
            }

            // If no valid x exists, store -1
            if (!found) {
                res.push_back(-1);
            }
        }

        // Return the constructed result array
        return res;
    }
};
```

## Test Cases Analysis

| Input       | Output       | Reasoning                     |        |
| ----------- | ------------ | ----------------------------- | ------ |
| `[3]`       | `[1]`        | `1                            | 2 = 3` |
| `[7]`       | `[3]`        | `3                            | 4 = 7` |
| `[5]`       | `[-1]`       | No valid pair                 |        |
| `[1, 2]`    | `[-1, -1]`   | No valid bitwise construction |        |
| `[3, 7, 5]` | `[1, 3, -1]` | Mixed valid and invalid cases |        |

## Edge Cases to Consider

* Very small values (`nums[i] = 1`)
* Numbers with sparse bit patterns
* Large values near the constraint limit
* Arrays of length `1`

## Common Test Cases

* Powers of two
* Numbers with consecutive set bits
* Random large integers

## Common Mistakes to Avoid

* Starting `x` from `0` unnecessarily
* Forgetting to stop after finding the minimum valid `x`
* Assuming a solution always exists

## Interview Relevance

* Tests understanding of bitwise OR operations
* Evaluates brute-force reasoning versus optimization
* Common in bit-manipulation interviews

## What This Problem Teaches

* How adjacent integers behave in bitwise operations
* Translating mathematical conditions into code
* Importance of early termination in brute-force solutions

## Key Takeaways

* Bitwise problems often require pattern observation
* Brute force can be acceptable under small constraints
* Always prioritize correctness before optimization

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes bitwise reasoning and direct simulation, making it suitable for beginners learning low-level operations and conditional logic.