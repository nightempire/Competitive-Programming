# Add Binary

## Platform

LeetCode

## Problem Link

[67. Add Binary](https://leetcode.com/problems/add-binary/)

## Problem Statement

You are given two binary strings `a` and `b`.

Your task is to return their **sum as a binary string**.

The strings consist only of characters `'0'` and `'1'`, and they represent non-negative binary numbers.

## Input Format

* Two strings `a` and `b`

  * Each string represents a binary number
  * The most significant bit is at the beginning of the string

## Output Format

* Return a string representing the **binary sum** of `a` and `b`

## Constraints

* `1 ≤ a.length, b.length ≤ 10^4`
* `a` and `b` consist only of `'0'` and `'1'`
* No leading zeros unless the string is `"0"`

## Examples

### Example 1

Input

```
a = "11"
b = "1"
```

Explanation

```
  11
+  1
----
 100
```

Output

```
"100"
```

### Example 2

Input

```
a = "1010"
b = "1011"
```

Explanation

```
 1010
+1011
-----
10101
```

Output

```
"10101"
```

## Approach

**Binary addition with carry (right-to-left traversal)**

## Intuition

Binary addition works exactly like decimal addition but with base `2`.

Key ideas:

* Start from the **least significant bit** (rightmost character)
* Add corresponding bits from both strings along with a carry
* Store the resulting bit and update the carry
* Continue until all bits and carry are processed

This mirrors manual binary addition.

## Algorithm Steps

* Initialize pointers at the end of both strings
* Initialize a carry variable
* While there are remaining bits in either string or a carry exists:

  * Extract the current bit from each string (if available)
  * Compute the sum of bits and carry
  * Append the resulting bit to the front of the result
  * Update the carry
* Return the final binary string

## Visual Walkthrough

### Test Case 1

Input:

```
a = "110"
b = "011"
```

Step-by-step:

```
0 + 1 = 1, carry = 0
1 + 1 = 0, carry = 1
1 + 0 + carry = 0, carry = 1
carry remains → add 1
```

Result:

```
1001
```

---

### Test Case 2

Input:

```
a = "0"
b = "0"
```

Result:

```
0
```

---

### Test Case 3

Input:

```
a = "111"
b = "1"
```

Result:

```
1000
```

## Complexity Analysis

### Time Complexity

**O(max(n, m))**

Each bit of both strings is processed exactly once, where:

* `n` = length of `a`
* `m` = length of `b`

### Space Complexity

**O(max(n, m))**

The result string stores at most one extra bit beyond the longer input string.

## Solution Explanation

The solution simulates binary addition starting from the least significant bits.
At each step, it:

* Converts characters `'0'` and `'1'` into integers
* Computes the sum including carry
* Prepends the resulting bit to the output string

The loop continues until all bits and any remaining carry are fully processed.

This ensures correctness for all input sizes and edge cases.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    string addBinary(string a, string b) {

        // Lengths of the two binary strings
        int p = a.length();
        int q = b.length();

        // Index used to traverse from the end
        int i = 0;

        // Result string
        string res = "";

        // Carry from binary addition
        bool carry = false;

        // Continue while bits remain or carry exists
        while (i < p || i < q || carry) {

            // Extract current bit from string a if available
            int x = (i < p) ? a[p - 1 - i] - '0' : 0;

            // Extract current bit from string b if available
            int y = (i < q) ? b[q - 1 - i] - '0' : 0;

            // Compute sum of bits and carry
            int sum = carry + x + y;

            // Append resulting bit to the front
            res = ((sum & 1) ? "1" : "0") + res;

            // Update carry
            carry = sum / 2;

            // Move to next bit
            i++;
        }

        return res;
    }
};
```

## Test Cases Analysis

| Test Case | a      | b      | Output  |
| --------- | ------ | ------ | ------- |
| 1         | "11"   | "1"    | "100"   |
| 2         | "1010" | "1011" | "10101" |
| 3         | "0"    | "0"    | "0"     |
| 4         | "111"  | "1"    | "1000"  |

## Edge Cases to Consider

* Both strings are `"0"`
* One string is significantly longer than the other
* Carry remains after processing all bits

## Common Test Cases

* Equal-length binary strings
* One-bit strings
* Inputs that produce an extra carry bit

## Common Mistakes to Avoid

* Traversing from left to right instead of right to left
* Forgetting to handle the final carry
* Incorrect character-to-integer conversion

## Interview Relevance

* Fundamental string manipulation problem
* Tests understanding of binary arithmetic
* Frequently asked in technical interviews

## What This Problem Teaches

* Simulation of arithmetic operations
* Handling carry in base-2 systems
* Careful index management in strings

## Key Takeaways

* Binary addition closely mirrors decimal addition
* Edge cases often involve carry handling
* Clean iteration avoids unnecessary conversions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic logic, careful iteration, and correct handling of edge cases rather than complex algorithms.