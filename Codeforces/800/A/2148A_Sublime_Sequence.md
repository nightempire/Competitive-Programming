# A_Sublime_Sequence

## Platform

Codeforces

## Problem Link

[A. Sublime Sequence](https://codeforces.com/problemset/problem/2148/A)

## Problem Statement

You are given two integers:

* `x`
* `n`

Consider a sequence where the value `x` is **XORed with itself `n` times**.

Your task is to determine the **final result of XORing `x` with itself `n` times**.

Formally, compute:

```text
x ⊕ x ⊕ x ⊕ ... ⊕ x   (n times)
```

Where `⊕` denotes the **bitwise XOR operation**.

For each test case, output the resulting value.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each of the next `t` lines contains two integers:

```
x n
```

## Output Format

For each test case, print a single integer — the result of XORing `x` with itself `n` times.

## Constraints

* `1 ≤ t ≤ 10^4`
* `0 ≤ x ≤ 10^9`
* `1 ≤ n ≤ 10^9`

## Examples

### Example 1

Input

```
3
5 1
5 2
5 3
```

Explanation

Case 1

```
5
```

Result

```
5
```

---

Case 2

```
5 ⊕ 5
```

Result

```
0
```

---

Case 3

```
5 ⊕ 5 ⊕ 5
```

Step-by-step

```
5 ⊕ 5 = 0
0 ⊕ 5 = 5
```

Result

```
5
```

Output

```
5
0
5
```

---

### Example 2

Input

```
2
7 4
9 5
```

Explanation

Case 1

```
7 ⊕ 7 ⊕ 7 ⊕ 7
```

Pair cancellations

```
(7 ⊕ 7) ⊕ (7 ⊕ 7) = 0 ⊕ 0
```

Result

```
0
```

Case 2

```
9 ⊕ 9 ⊕ 9 ⊕ 9 ⊕ 9
```

```
(9 ⊕ 9) ⊕ (9 ⊕ 9) ⊕ 9
```

```
0 ⊕ 0 ⊕ 9
```

Result

```
9
```

Output

```
0
9
```

---

### Example 3

Input

```
2
10 6
10 7
```

Explanation

Case 1

```
10 ⊕ 10 ⊕ 10 ⊕ 10 ⊕ 10 ⊕ 10
```

Even occurrences cancel out.

Result

```
0
```

Case 2

```
10 ⊕ 10 ⊕ 10 ⊕ 10 ⊕ 10 ⊕ 10 ⊕ 10
```

Pairs cancel leaving one `10`.

Result

```
10
```

Output

```
0
10
```

## Approach

Bitwise XOR Property Observation

## Intuition

The XOR operation has an important property:

```
a ⊕ a = 0
```

And

```
a ⊕ 0 = a
```

Therefore:

* Two identical numbers XOR to **0**.
* XORing a number with itself **even times cancels out completely**.
* XORing a number **odd times leaves one copy of the number**.

Thus:

```
x ⊕ x ⊕ x ⊕ ... (n times)
```

If `n` is **even**

```
result = 0
```

If `n` is **odd**

```
result = x
```

This eliminates the need for repeated XOR operations.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read `x` and `n`.
  * If `n` is odd:

    * Print `x`.
  * Otherwise:

    * Print `0`.

## Visual Walkthrough

### Test Case 1

Input

```
x = 6
n = 2
```

Expression

```
6 ⊕ 6
```

Result

```
0
```

---

### Test Case 2

Input

```
x = 6
n = 3
```

Expression

```
6 ⊕ 6 ⊕ 6
```

Step-by-step

```
6 ⊕ 6 = 0
0 ⊕ 6 = 6
```

Result

```
6
```

---

### Test Case 3

Input

```
x = 8
n = 5
```

Expression

```
8 ⊕ 8 ⊕ 8 ⊕ 8 ⊕ 8
```

Pairs cancel

```
(8 ⊕ 8) ⊕ (8 ⊕ 8) ⊕ 8
```

Result

```
8
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case requires only a parity check.

### Space Complexity

O(1)

Only a few variables are used.

## Solution Explanation

Instead of performing `n` XOR operations, the program uses the mathematical property of XOR cancellation.

It checks whether `n` is odd using a bitwise operation:

```
n & 1
```

If the result is `1`, `n` is odd and the answer is `x`.
Otherwise, the answer is `0`.

This makes the solution extremely efficient even for large `n`.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t, x, n;

    cin >> t;

    while (t--) {

        // Read values
        cin >> x >> n;

        // If n is odd → result = x
        // If n is even → result = 0
        cout << (n & 1 ? x : 0) << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| x | n | XOR Result |
| - | - | ---------- |
| 5 | 1 | 5          |
| 5 | 2 | 0          |
| 5 | 3 | 5          |
| 7 | 4 | 0          |
| 9 | 5 | 9          |

## Edge Cases to Consider

* `n = 1`
* `n` very large (`10^9`)
* `x = 0`
* Large values of `x`

## Common Test Cases

* `5 2`
* `5 3`
* `10 6`
* `10 7`
* `0 5`

## Common Mistakes to Avoid

* Attempting to simulate XOR `n` times
* Forgetting XOR cancellation properties
* Incorrect parity checks

## Interview Relevance

* Tests knowledge of XOR properties
* Demonstrates bitwise optimization
* Encourages mathematical simplification

## What This Problem Teaches

* Understanding XOR cancellation rules
* Recognizing patterns in repeated operations
* Using parity checks for optimization

## Key Takeaways

* XOR of identical numbers cancels in pairs
* Even repetitions produce `0`
* Odd repetitions produce the original number

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The challenge lies in recognizing the XOR cancellation property. Once identified, the implementation becomes a simple parity check.