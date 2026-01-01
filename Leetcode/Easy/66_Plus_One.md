# 66. Plus One

## Platform

LeetCode

## Problem Link

[66. Plus One](https://leetcode.com/problems/plus-one/)

## Problem Statement

You are given a **large integer** represented as an array of digits, where each element contains a single digit.
The digits are ordered from most significant to least significant.

Increment the integer by **one** and return the resulting array of digits.

You may assume the integer does not contain leading zeros.

## Input Format

* A vector of integers `digits`

  * Each element is in the range `0–9`
  * Most significant digit comes first

## Output Format

* A vector of integers representing the incremented number

## Constraints

* `1 ≤ digits.length ≤ 100`
* `0 ≤ digits[i] ≤ 9`
* No leading zeros in the input

## Examples

### Example 1

Input

```
[1, 2, 3]
```

Explanation

```
123 + 1 = 124
```

Output

```
[1, 2, 4]
```

### Example 2

Input

```
[4, 3, 2, 1]
```

Explanation

```
4321 + 1 = 4322
```

Output

```
[4, 3, 2, 2]
```

### Example 3

Input

```
[9, 9, 9]
```

Explanation

```
999 + 1 = 1000
```

Output

```
[1, 0, 0, 0]
```

## Approach

**Digit-wise Addition with Carry Propagation**

## Intuition

Adding one to a number behaves differently depending on the last digit:

* If the last digit is less than `9`, simply increment it.
* If the last digit is `9`, it becomes `0` and produces a carry.
* The carry may propagate toward the most significant digit.
* If all digits are `9`, a new digit `1` must be added at the front.

This mimics elementary addition from right to left.

## Algorithm Steps

* Traverse the digits array from right to left
* If the current digit is less than `9`:

  * Increment it
  * Return the result immediately
* Otherwise:

  * Set the digit to `0` and continue
* If all digits were `9`:

  * Create a new array with one extra digit
  * Set the first digit to `1`
* Return the new array

## Visual Walkthrough

Input:

```
[9, 9, 9]
```

Step-by-step:

```
Rightmost 9 → becomes 0 (carry)
Next 9     → becomes 0 (carry)
Next 9     → becomes 0 (carry)
```

All digits exhausted, create:

```
[1, 0, 0, 0]
```

Another case:

```
[1, 2, 8]
```

```
8 < 9 → increment → [1, 2, 9]
```

## Complexity Analysis

### Time Complexity

O(n)

In the worst case, all digits are processed once.

### Space Complexity

O(n)

Additional space is used only when all digits are `9`.

## Solution Explanation

The solution simulates manual addition.
By iterating from the least significant digit and handling carry propagation, it efficiently handles all cases, including numbers composed entirely of `9`s.
Early termination ensures optimal performance when no full carry chain is required.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {

        // Traverse digits from the least significant position
        for (int i = digits.size() - 1; i >= 0; i--) {

            // If the current digit is less than 9,
            // simply increment it and return the result
            if (digits[i] < 9) {
                digits[i]++;
                return digits;
            }

            // If the digit is 9, it becomes 0 due to carry
            digits[i] = 0;
        }

        // If all digits were 9, we need an extra digit
        vector<int> res(digits.size() + 1, 0);

        // Set the most significant digit to 1
        res[0] = 1;

        return res;
    }
};
```

## Test Cases Analysis

| Input     | Output    |
| --------- | --------- |
| [1,2,3]   | [1,2,4]   |
| [9]       | [1,0]     |
| [9,9]     | [1,0,0]   |
| [4,3,2,1] | [4,3,2,2] |

## Edge Cases to Consider

* Single digit equal to `9`
* All digits equal to `9`
* Large digit arrays

## Common Test Cases

* No carry required
* Carry propagates partially
* Carry propagates through all digits

## Common Mistakes to Avoid

* Converting digits to an integer (risk of overflow)
* Forgetting to handle all-`9` cases
* Iterating in the wrong direction

## Interview Relevance

* Frequently asked array manipulation problem
* Tests carry handling logic
* Evaluates in-place modification skills

## What This Problem Teaches

* Simulating arithmetic using arrays
* Handling edge cases cleanly
* Writing efficient early-exit logic

## Key Takeaways

* Always process digits from right to left
* Carry propagation is the core challenge
* Avoid unnecessary conversions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on array traversal and arithmetic simulation, making it a common screening and interview warm-up question.