# 1404. Number of Steps to Reduce a Number in Binary Representation to One

## Platform

LeetCode

## Problem Link

[1404. Number of Steps to Reduce a Number in Binary Representation to One](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-in-binary-representation-to-one/)

---

## Problem Statement

You are given a binary string `s` representing a positive integer.

You must perform the following operations until the number becomes `1`:

* If the number is **even** → divide it by 2.
* If the number is **odd** → add 1 to it.

Return the total number of steps required to reduce the number to `1`.

---

## Input Format

* A binary string `s`.
* `s` contains only `'0'` and `'1'`.
* The most significant bit is guaranteed to be `'1'`.

---

## Output Format

* Return an integer representing the number of operations needed.

---

## Constraints

* `1 ≤ s.length ≤ 500`
* `s[0] == '1'`

---

## Examples

### Example 1

Input

```
s = "1101"
```

Binary representation:

```
13 (decimal)
```

Steps:

| Operation | Binary | Decimal |
| --------- | ------ | ------- |
| Odd → +1  | 1110   | 14      |
| Even → /2 | 111    | 7       |
| Odd → +1  | 1000   | 8       |
| Even → /2 | 100    | 4       |
| Even → /2 | 10     | 2       |
| Even → /2 | 1      | 1       |

Total steps = **6**

---

### Example 2

Input

```
s = "10"
```

Steps:

```
10 → 1
```

Total steps = **1**

---

### Example 3

Input

```
s = "1"
```

Already 1 → steps = **0**

---

## Approach (Algorithm Type)

**Binary Simulation using String Manipulation**

---

## Intuition

Binary properties:

* If last bit is `'0'` → number is even → divide by 2 → remove last bit.
* If last bit is `'1'` → number is odd → add 1 → simulate binary addition.

So the logic becomes:

* While string length > 1:

  * If last character is `'0'` → pop back.
  * Else → simulate binary addition with carry.

Repeat until string becomes `"1"`.

---

## Key Observations

Division by 2 in binary:

```
Right shift → remove last bit
```

Adding 1 in binary:

* Traverse from right to left.
* Flip consecutive `'1'` to `'0'`.
* Change first `'0'` to `'1'`.
* If all bits were `'1'`, prepend `'1'`.

---

## Algorithm Steps

* Initialize `ops = 0`.
* While `s.length() > 1`:

  * If last character is `'0'`:

    * Remove last character.
  * Else:

    * Perform binary addition of 1.
  * Increment `ops`.
* Return `ops`.

---

## Visual Walkthrough

### Test Case 1

Input:

```
"1101"
```

Process:

```
1101 (odd) → add 1 → 1110
1110 (even) → shift → 111
111 (odd) → add 1 → 1000
1000 (even) → shift → 100
100 (even) → shift → 10
10 (even) → shift → 1
```

Total operations = **6**

---

### Test Case 2

Input:

```
"101"
```

Process:

```
101 (odd) → 110
110 (even) → 11
11 (odd) → 100
100 (even) → 10
10 (even) → 1
```

Total operations = **5**

---

### Test Case 3

Input:

```
"1000"
```

Process:

```
1000 → 100 → 10 → 1
```

Total operations = **3**

---

## Complexity Analysis

### Time Complexity

Worst case:

* Each add operation may traverse entire string.
* Length ≤ 500.

Worst-case scenario:

```
O(n^2)
```

However, practical behavior is closer to:

```
O(n)
```

Because each bit is flipped at most a constant number of times.

---

### Space Complexity

```
O(1)
```

No extra data structures used (modifying input string).

---

## Solution Explanation

The solution defines two helper functions:

* `rightShift()` → removes last bit (division by 2).
* `addOne()` → simulates binary addition with carry handling.

Main loop:

* Continues until the string reduces to `"1"`.
* Applies correct operation based on parity.
* Counts operations.

This directly simulates the problem statement.

---

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:

    // Function to simulate division by 2
    // Removes the last bit of the binary string
    void rightShift(string& s) {
        s.pop_back();
    }

    // Function to simulate adding 1 to a binary number
    void addOne(string& s) {

        int n = s.length();
        int i = n - 1;

        // Traverse from right to left while encountering '1'
        // Flip '1' to '0' to handle carry
        while(i >= 0 && s[i] != '0') {
            s[i] = '0';
            i--;
        }

        // If all bits were '1'
        // We need to add a new leading '1'
        if(i == -1) {
            s = "1" + s;
        }
        else {
            // Replace first '0' with '1'
            s[i] = '1';
        }
    }

    int numSteps(string s) {

        int ops = 0;

        // Continue until string becomes "1"
        while(s.length() > 1) {

            // If even
            if(s.back() == '0') {
                rightShift(s);
            }
            // If odd
            else {
                addOne(s);
            }

            ops++;
        }

        return ops;
    }
};
```

---

## Test Cases Analysis

| Input  | Steps |
| ------ | ----- |
| "1"    | 0     |
| "10"   | 1     |
| "11"   | 3     |
| "101"  | 5     |
| "1101" | 6     |
| "1000" | 3     |

---

## Edge Cases to Consider

* Input is already `"1"`
* All bits are `'1'`
* Very long binary string (length 500)
* Single `'1'` followed by many zeros

---

## Common Test Cases

* Power of two
* Alternating bits
* All ones
* Large binary number

---

## Common Mistakes to Avoid

* Incorrect carry handling
* Infinite loop when string becomes `"1"`
* Not handling all-ones case

---

## Interview Relevance

* Tests binary arithmetic understanding
* Requires careful simulation
* Demonstrates carry handling logic

---

## What This Problem Teaches

* Binary number manipulation
* Efficient string simulation
* Handling edge cases in arithmetic operations

---

## Key Takeaways

* Division by 2 in binary is a right shift.
* Adding 1 requires proper carry handling.
* Simulation problems require precise implementation.

---

## Problem Difficulty Analysis

This is a **Medium-level** LeetCode problem.

While conceptually simple, correct implementation of binary addition and understanding time complexity requires careful reasoning.