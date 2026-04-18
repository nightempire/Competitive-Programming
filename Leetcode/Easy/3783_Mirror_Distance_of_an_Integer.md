## Platform

LeetCode

## Problem Link

[3783. Mirror Distance of an Integer](https://leetcode.com/problems/mirror-distance-of-an-integer)

---

## Problem Statement

You are given an integer `n`.

Define the **mirror** of `n` as the integer obtained by reversing its digits.

Your task is to compute the **mirror distance**, defined as:

```text
|n - reverse(n)|
```

Return this absolute difference.

---

## Input Format

* An integer `n`

---

## Output Format

* Return an integer — the mirror distance

---

## Constraints

* `0 ≤ n ≤ 10^9`

---

## Examples

### Example 1

Input

```
n = 123
```

Explanation

* Reverse = `321`
* Distance = `|123 - 321| = 198`

Output

```
198
```

---

### Example 2

Input

```
n = 100
```

Explanation

* Reverse = `1`
* Distance = `|100 - 1| = 99`

Output

```
99
```

---

### Example 3

Input

```
n = 7
```

Explanation

* Reverse = `7`
* Distance = `|7 - 7| = 0`

Output

```
0
```

---

## Approach

Digit reversal + absolute difference

---

## Intuition

To compute the mirror distance:

* Reverse the digits of `n`
* Compute the absolute difference between original and reversed number

---

## Algorithm Steps

* Initialize `rev = 0`
* Copy `n` into `temp`
* While `temp > 0`:

  * Extract last digit:

    ```
    digit = temp % 10
    ```
  * Append to reversed number:

    ```
    rev = rev * 10 + digit
    ```
  * Remove last digit:

    ```
    temp /= 10
    ```
* Return:

  ```
  abs(n - rev)
  ```

---

## Visual Walkthrough

### Case 1: `n = 123`

```
Step 1: rev = 3
Step 2: rev = 32
Step 3: rev = 321

Distance = |123 - 321| = 198
```

---

### Case 2: `n = 100`

```
Step 1: rev = 0
Step 2: rev = 0
Step 3: rev = 1

Distance = |100 - 1| = 99
```

---

### Case 3: `n = 7`

```
rev = 7

Distance = 0
```

---

## Complexity Analysis

### Time Complexity

O(d)

* Where `d` is number of digits in `n` (≤ 10)

---

### Space Complexity

O(1)

* Only a few variables used

---

## Solution Explanation

The solution reverses the digits using standard arithmetic operations and computes the absolute difference.

This avoids string conversion and ensures optimal performance.

---

## Full Solution

### C++ Implementation

```cpp
#include <cmath>
using namespace std;

class Solution {
public:
    int mirrorDistance(int n) {

        // Variable to store reversed number
        int rev = 0;

        // Temporary variable for processing
        int temp = n;

        // Reverse the digits
        while(temp) {

            // Extract last digit and append to rev
            rev = rev * 10 + temp % 10;

            // Remove last digit
            temp /= 10;
        }

        // Return absolute difference
        return abs(n - rev);
    }
};
```

---

## Test Cases Analysis

| n   | Reverse | Distance |
| --- | ------- | -------- |
| 123 | 321     | 198      |
| 100 | 1       | 99       |
| 7   | 7       | 0        |
| 909 | 909     | 0        |

---

## Edge Cases to Consider

* `n = 0`
* Numbers ending with zeros
* Palindrome numbers
* Single-digit numbers

---

## Common Test Cases

* `n = 10` → 9
* `n = 121` → 0
* `n = 1000` → 999

---

## Common Mistakes to Avoid

* Not handling trailing zeros correctly
* Using string conversion unnecessarily
* Forgetting absolute value

---

## Interview Relevance

* Number manipulation
* Digit extraction techniques
* Efficient arithmetic operations

---

## What This Problem Teaches

* How to reverse digits mathematically
* Handling integer transformations
* Writing efficient low-level logic

---

## Key Takeaways

* Use `%` and `/` for digit operations
* Always use `abs()` for distance
* Avoid unnecessary conversions

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Arithmetic operations
* Digit manipulation
* Basic problem solving