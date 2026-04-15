## Platform

Codeforces

## Problem Link

[A. System of Equations](https://codeforces.com/problemset/problem/214/A)

---

## Problem Statement

You are given two integers `n` and `m`.

Find the number of pairs `(a, b)` of **non-negative integers** that satisfy the system:

```text
a² + b = n  
a + b² = m
```

---

## Input Format

* A single line containing two integers `n` and `m`

---

## Output Format

* Print a single integer — the number of valid pairs `(a, b)`

---

## Constraints

* `0 ≤ n, m ≤ 1000`

---

## Examples

### Example 1

Input

```
9 3
```

Explanation

Check possible values:

* `(a, b) = (3, 0)`:

  * `3² + 0 = 9`
  * `3 + 0² = 3` ✔

Output

```
1
```

---

### Example 2

Input

```
14 28
```

Explanation

* `(a, b) = (3, 5)`:

  * `9 + 5 = 14`
  * `3 + 25 = 28` ✔

Output

```
1
```

---

### Example 3

Input

```
4 20
```

Explanation

* `(a, b) = (0, 4)`:

  * `0 + 4 = 4`
  * `0 + 16 = 16 ≠ 20` ✘

No valid pairs

Output

```
0
```

---

## Approach

Brute-force with constraint optimization

---

## Intuition

From the first equation:

```text
b = n - a²
```

We substitute into the second equation:

```text
a + (n - a²)² = m
```

Instead of solving algebraically, we can:

* Iterate over all possible values of `a`
* Compute `b`
* Check if second equation holds

---

## Algorithm Steps

* Read `n` and `m`
* Initialize `count = 0`
* Loop `a` from `0` while `a² ≤ n`:

  * Compute:

    ```
    b = n - a²
    ```
  * Check:

    ```
    a + b² == m
    ```
  * If true:

    * Increment `count`
* Print `count`

---

## Visual Walkthrough

### Case 1: `n = 9, m = 3`

```
a = 0 → b = 9 → 0 + 81 = 81 ≠ 3
a = 1 → b = 8 → 1 + 64 = 65 ≠ 3
a = 2 → b = 5 → 2 + 25 = 27 ≠ 3
a = 3 → b = 0 → 3 + 0 = 3 ✔
```

Result → `1`

---

### Case 2: `n = 14, m = 28`

```
a = 3 → b = 5
Check:
3 + 25 = 28 ✔
```

---

### Case 3: `n = 4, m = 20`

```
a = 0 → b = 4 → 0 + 16 = 16 ≠ 20
a = 1 → b = 3 → 1 + 9 = 10 ≠ 20
a = 2 → b = 0 → 2 + 0 = 2 ≠ 20
```

Result → `0`

---

## Complexity Analysis

### Time Complexity

O(√n)

* Loop runs while `a² ≤ n`

---

### Space Complexity

O(1)

* Only variables used

---

## Solution Explanation

The solution uses a simple brute-force approach:

* Iterate possible values of `a`
* Compute corresponding `b`
* Validate both equations

Since constraints are small (`≤ 1000`), this approach is efficient.

---

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Input values
    int n, m, count = 0;
    cin >> n >> m;

    // Iterate over possible values of a
    for(int a = 0; a * a <= n; a++) {

        // Compute corresponding b
        int b = n - a * a;

        // Check second equation
        if(a + b * b == m) {
            count++;
        }
    }

    // Output result
    cout << count << '\n';

    return 0;
}
```

---

## Test Cases Analysis

| n  | m  | Valid Pairs | Output |
| -- | -- | ----------- | ------ |
| 9  | 3  | (3,0)       | 1      |
| 14 | 28 | (3,5)       | 1      |
| 4  | 20 | None        | 0      |

---

## Edge Cases to Consider

* `n = 0`, `m = 0`
* Only one valid pair
* No valid pairs
* Maximum constraint values

---

## Common Test Cases

* Small values (`n, m ≤ 10`)
* Equal values
* No solution cases

---

## Common Mistakes to Avoid

* Iterating beyond valid range
* Forgetting `b ≥ 0` (automatically ensured here)
* Not checking both equations

---

## Interview Relevance

* Brute-force optimization
* Mathematical substitution
* Constraint-based iteration

---

## What This Problem Teaches

* Reducing equations using substitution
* Efficient iteration bounds
* Validating multiple conditions

---

## Key Takeaways

* Limit search space using constraints
* Substitute variables to simplify problem
* Brute force can be optimal for small limits

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Mathematical reasoning
* Loop optimization
* Condition checking