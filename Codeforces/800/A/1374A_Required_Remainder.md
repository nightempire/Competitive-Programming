# A_Required_Remainder

## Platform

Codeforces

## Problem Link

[A. Required Remainder](https://codeforces.com/problemset/problem/1374/A)

## Problem Statement

You are given three integers `x`, `y`, and `n`.

Your task is to find the **maximum integer `k`** such that:

* `0 ≤ k ≤ n`
* `k mod x = y`

It is guaranteed that a solution always exists.

Each test case is independent.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * Three integers `x`, `y`, and `n`.

## Output Format

* For each test case, print the value of `k` that satisfies the conditions.

## Constraints

* `1 ≤ t ≤ 10⁴`
* `1 ≤ x ≤ 10⁹`
* `0 ≤ y < x`
* `0 ≤ n ≤ 10⁹`

## Examples

### Example 1

Input

```
3
7 5 12345
5 0 4
10 5 15
```

Explanation

* `(7, 5, 12345)` → `12339 mod 7 = 5`
* `(5, 0, 4)` → `0 mod 5 = 0`
* `(10, 5, 15)` → `15 mod 10 = 5`

Output

```
12339
0
15
```

---

### Example 2

Input

```
1
4 2 11
```

Explanation

* Largest `k ≤ 11` such that `k mod 4 = 2` is `10`

Output

```
10
```

## Approach

**Mathematical Formula-Based Optimization**

## Intuition

Any number `k` that satisfies:

```
k mod x = y
```

can be written as:

```
k = x * m + y
```

To maximize `k` while keeping `k ≤ n`, we must choose the **largest possible `m`** such that:

```
x * m + y ≤ n
```

Solving for `m` gives:

```
m = ⌊(n - y) / x⌋
```

## Algorithm Steps

* Read number of test cases `t`.
* For each test case:

  * Read integers `x`, `y`, and `n`.
  * Compute:

    ```
    k = ((n - y) / x) * x + y
    ```
  * Output `k`.

## Visual Walkthrough

### Test Case: `x = 7, y = 5, n = 12345`

```
n - y = 12340
(12340 / 7) = 1762
k = 1762 * 7 + 5 = 12339
```

---

### Test Case: `x = 4, y = 2, n = 11`

```
n - y = 9
(9 / 4) = 2
k = 2 * 4 + 2 = 10
```

## Complexity Analysis

### Time Complexity

**O(1) per test case**

* Only arithmetic operations are used.

### Space Complexity

**O(1)**

* No extra memory required.

## Solution Explanation

The solution directly applies modular arithmetic properties to compute the answer in constant time.

Instead of iterating or checking multiple values, it computes the largest valid multiplier of `x` that keeps the result within the limit `n`, then adds the required remainder `y`.

This guarantees both correctness and efficiency.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while (t--) {

        int x, y, n;
        cin >> x >> y >> n;

        // Compute the maximum k such that k % x == y and k <= n
        int ans = (n - y) / x * x + y;

        cout << ans << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| x  | y | n     | Output |
| -- | - | ----- | ------ |
| 7  | 5 | 12345 | 12339  |
| 5  | 0 | 4     | 0      |
| 10 | 5 | 15    | 15     |
| 4  | 2 | 11    | 10     |

## Edge Cases to Consider

* `y = 0`
* `n < x`
* Large values of `x` and `n`

## Common Test Cases

* Random large inputs
* Boundary cases where `k = n`
* Minimum valid values

## Common Mistakes to Avoid

* Using brute force iteration
* Forgetting integer division behavior
* Misinterpreting modulo conditions

## Interview Relevance

* Tests understanding of modular arithmetic
* Evaluates optimization and math skills
* Common problem in coding assessments

## What This Problem Teaches

* Efficient use of mathematical formulas
* Translating constraints into equations
* Avoiding unnecessary loops

## Key Takeaways

* Modular constraints often reduce to simple equations
* Constant-time solutions are preferable
* Understanding integer division is crucial

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on mathematical reasoning and efficient implementation.