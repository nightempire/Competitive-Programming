## Platform

Codeforces

## Problem Link

[A. Park Lighting](https://codeforces.com/problemset/problem/1358/A)

---

## Problem Statement

You are given a rectangular grid of size `n × m`.

Each cell represents a position in a park. You want to place lights such that:

* Each light illuminates its own cell
* A light can also illuminate adjacent cells

The constraint is:

* No two lights should be placed in adjacent cells (to avoid overlap)

Your task is to determine the **minimum number of lights required** to illuminate the entire park.

---

## Input Format

* The first line contains an integer `t` — number of test cases
* For each test case:

  * Two integers `n` and `m`

---

## Output Format

For each test case:

* Print a single integer — minimum number of lights required

---

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n, m ≤ 10^9`

---

## Examples

### Example 1

Input

```id="g8l2pq"
3
1 1
2 2
3 3
```

Explanation

* `1×1` → 1 cell → need 1 light
* `2×2` → 4 cells → need 2 lights
* `3×3` → 9 cells → need 5 lights

Output

```id="k3x9wn"
1
2
5
```

---

### Example 2

Input

```id="n5m2ts"
2
2 3
4 5
```

Explanation

* `2×3 = 6` cells → need 3 lights
* `4×5 = 20` cells → need 10 lights

Output

```id="t2v8hz"
3
10
```

---

### Example 3

Input

```id="x7c9ld"
1
5 5
```

Explanation

* Total cells = 25 → need 13 lights

Output

```id="u6k4ra"
13
```

---

## Approach

Mathematical observation (ceiling of half the cells)

---

## Intuition

To ensure no two lights are adjacent:

* Place lights in a **checkerboard pattern**

This ensures:

* No two lights touch each other
* Maximum coverage with minimum lights

Thus, we place lights in approximately **half of the cells**

---

## Key Formula

```text id="7n3j2p"
Required lights = ceil(n × m / 2)
```

Which is implemented as:

```text id="4v8m1x"
(n * m + 1) / 2
```

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `n` and `m`
  * Compute:

    ```
    result = (n * m + 1) / 2
    ```
  * Print result

---

## Visual Walkthrough

### Case 1: `2 × 2`

```id="w8z3po"
Grid:
. #
# .

Lights = 2
```

---

### Case 2: `3 × 3`

```id="h4t7kd"
# . #
. # .
# . #

Lights = 5
```

---

### Case 3: `2 × 3`

```id="z1p9mv"
# . #
. # .

Lights = 3
```

---

## Complexity Analysis

### Time Complexity

O(1) per test case

* Direct formula computation

---

### Space Complexity

O(1)

* No extra space used

---

## Solution Explanation

The problem reduces to placing lights in such a way that no two are adjacent.

A checkerboard pattern achieves this optimally.

Thus, the number of lights required is simply half the cells (rounded up).

---

## Full Solution

### C++ Implementation

```cpp id="r8k3mz"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Grid dimensions
        int n, m;
        cin >> n >> m;

        // Compute minimum lights using formula
        cout << (n * m + 1) / 2 << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| n | m | Total Cells | Lights Needed |
| - | - | ----------- | ------------- |
| 1 | 1 | 1           | 1             |
| 2 | 2 | 4           | 2             |
| 3 | 3 | 9           | 5             |
| 2 | 3 | 6           | 3             |
| 5 | 5 | 25          | 13            |

---

## Edge Cases to Consider

* `n = 1` or `m = 1`
* Very large values (`10^9`)
* Odd vs even number of cells

---

## Common Test Cases

* Single row grid
* Square grid
* Rectangular grid

---

## Common Mistakes to Avoid

* Using integer division without rounding up
* Overcomplicating with grid simulation
* Forgetting large input constraints

---

## Interview Relevance

* Mathematical optimization
* Pattern recognition
* Efficient problem solving

---

## What This Problem Teaches

* Converting grid problems into math formulas
* Using ceiling division effectively
* Recognizing checkerboard patterns

---

## Key Takeaways

* Optimal placement often follows patterns
* Use `(x + 1) / 2` for ceiling division
* Avoid simulation when formula exists

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Mathematical reasoning
* Pattern recognition
* Efficient computation