# A. Calculating Function

## Platform

Codeforces

## Problem Link

[A. Calculating Function](https://codeforces.com/problemset/problem/486/A)

## Problem Statement

You are given an integer `n`.

Define a function `f(n)` as follows:

* Add all **even** numbers from `1` to `n`
* Subtract all **odd** numbers from `1` to `n`

Your task is to compute the value of this function efficiently.

## Input Format

* A single integer `n`

## Output Format

Print the value of `f(n)`.

## Constraints

* `1 ≤ n ≤ 10^15`

## Examples

### Example 1

Input

```
1
```

Explanation

Odd numbers: `1`
Even numbers: none

Result:

```
0 - 1 = -1
```

Output

```
-1
```

### Example 2

Input

```
4
```

Explanation

Odd numbers: `1 + 3 = 4`
Even numbers: `2 + 4 = 6`

Result:

```
6 - 4 = 2
```

Output

```
2
```

## Approach

Mathematical observation using parity of `n`.

## Intuition

Instead of iterating from `1` to `n`, observe the pattern:

* If `n` is **even**, the sum of evens exceeds the sum of odds by `n / 2`
* If `n` is **odd**, the sum of odds exceeds the sum of evens by `(n + 1) / 2`

This allows the result to be computed in **constant time**, even for very large values of `n`.

## Algorithm Steps

* Read integer `n`
* Check whether `n` is odd or even
* If `n` is even:

  * Output `n / 2`
* If `n` is odd:

  * Output `- (n + 1) / 2`

## Visual Walkthrough

For `n = 5`:

```
Odd numbers: 1, 3, 5  → sum = 9
Even numbers: 2, 4    → sum = 6
```

Final value:

```
6 - 9 = -3
```

Computed directly as:

```
- (5 + 1) / 2 = -3
```

## Complexity Analysis

### Time Complexity

**O(1)**
Only a constant number of operations are performed.

### Space Complexity

**O(1)**
No extra memory is used.

## Solution Explanation

The solution relies on recognizing a mathematical pattern instead of brute-force summation.

Using bitwise operation `n & 1`, the program checks whether `n` is odd.
Based on parity, it directly prints the computed result using a closed-form expression.

This ensures correctness, efficiency, and scalability for very large inputs.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Input number
    long long n;

    // Read input
    cin >> n;

    // If n is odd
    if (n & 1)
        cout << - (n + 1) / 2 << endl;
    else
        // If n is even
        cout << n / 2 << endl;

    return 0;
}
```

## Test Cases Analysis

| n     | Output | Reasoning                 |
| ----- | ------ | ------------------------- |
| 1     | -1     | Single odd number         |
| 2     | 1      | 2 - 1 = 1                 |
| 3     | -2     | (2) - (1 + 3)             |
| 4     | 2      | (2 + 4) - (1 + 3)         |
| 10^15 | Valid  | Computed in constant time |

## Edge Cases to Consider

* Minimum value (`n = 1`)
* Very large values of `n`
* Transition between odd and even values

## Common Test Cases

* Small even numbers
* Small odd numbers
* Large boundary values

## Common Mistakes to Avoid

* Using loops for summation (inefficient)
* Incorrect handling of odd values
* Integer overflow by using smaller data types

## Interview Relevance

* Tests mathematical reasoning
* Evaluates ability to optimize brute-force logic
* Common problem for assessing time complexity awareness

## What This Problem Teaches

* Importance of pattern recognition
* Using mathematics to reduce complexity
* Efficient handling of large inputs

## Key Takeaways

* Mathematical formulas can replace loops
* Always check constraints before choosing an approach
* Constant-time solutions are ideal for large ranges

## Problem Difficulty Analysis

This is an **Easy-level** problem.

Although simple in logic, it emphasizes mathematical insight and optimization, making it a good test of problem-solving skills.