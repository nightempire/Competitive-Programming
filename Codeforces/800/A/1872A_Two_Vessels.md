## Platform

Codeforces

## Problem Link

[A. Two Vessels](https://codeforces.com/problemset/problem/1872/A)

---

## Problem Statement

You are given two vessels containing `a` and `b` units of water.

You can perform the following operation:

* In one move, you can transfer at most `c` units of water from one vessel to the other

Your goal is to make the amounts of water in both vessels **equal**.

Determine the **minimum number of operations** required.

---

## Input Format

* The first line contains an integer `t` — number of test cases
* For each test case:

  * Three integers `a`, `b`, and `c`

---

## Output Format

For each test case:

* Print a single integer — minimum number of operations

---

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ a, b, c ≤ 10^9`

---

## Examples

### Example 1

Input

```id="w5k2qp"
3
10 20 5
8 4 2
7 7 3
```

Explanation

* Case 1:

  * Difference = 10 → need to balance 5 units
  * Each move handles 5 → 1 move
* Case 2:

  * Difference = 4 → balance = 2
  * Each move handles 2 → 1 move
* Case 3:

  * Already equal → 0 moves

Output

```id="z2m9tl"
1
1
0
```

---

### Example 2

Input

```id="g8q4nx"
2
1 10 3
100 1 10
```

Explanation

* Case 1:

  * Difference = 9 → balance = 4.5 → ceil(4.5/3) = 2
* Case 2:

  * Difference = 99 → balance = 49.5 → ceil(49.5/10) = 5

Output

```id="p6v3ys"
2
5
```

---

### Example 3

Input

```id="y3c7rh"
1
5 9 1
```

Explanation

* Difference = 4 → balance = 2
* Each move = 1 → 2 moves

Output

```id="n4k8xp"
2
```

---

## Approach

Mathematical calculation with ceiling division

---

## Intuition

To equalize:

* Let difference = `|a - b|`
* We need to move **half of the difference**:

```text id="t2p8cx"
balance = |a - b| / 2
```

Each operation can move at most `c` units, so:

```text id="v7k1mz"
operations = ceil(balance / c)
```

---

## Key Formula

```text id="q9x3dv"
Answer = ceil( |a - b| / (2 × c) )
```

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `a`, `b`, `c`
  * Compute:

    ```
    diff = abs(a - b)
    balance = diff / 2.0
    result = ceil(balance / c)
    ```
  * Print result

---

## Visual Walkthrough

### Case 1: `a = 10, b = 20, c = 5`

```id="r3m8sz"
Difference = 10
Balance = 5
Each move = 5

Moves = 1
```

---

### Case 2: `a = 1, b = 10, c = 3`

```id="z6k4pw"
Difference = 9
Balance = 4.5

Moves = ceil(4.5 / 3) = 2
```

---

### Case 3: `a = 7, b = 7`

```id="k5x9nd"
Already equal → 0 moves
```

---

## Complexity Analysis

### Time Complexity

O(1) per test case

* Only arithmetic operations

---

### Space Complexity

O(1)

* No extra memory used

---

## Solution Explanation

The problem reduces to distributing the difference evenly.

Instead of simulating transfers:

* Compute how much imbalance exists
* Divide by the maximum transfer per move
* Use ceiling to handle partial transfers

---

## Full Solution

### C++ Implementation

```cpp id="v8m2rp"
#include<iostream>
#include<cmath>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input values
        int a, b, c;
        cin >> a >> b >> c;

        // Calculate half of the difference
        float balance = abs(a - b) / 2.0;

        // Compute minimum operations using ceiling
        cout << ceil(balance / c) << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| a  | b  | c | Difference | Moves |
| -- | -- | - | ---------- | ----- |
| 10 | 20 | 5 | 10         | 1     |
| 8  | 4  | 2 | 4          | 1     |
| 1  | 10 | 3 | 9          | 2     |
| 7  | 7  | 3 | 0          | 0     |

---

## Edge Cases to Consider

* `a == b` → 0 moves
* Large differences
* `c = 1` (smallest transfer)

---

## Common Test Cases

* Equal values
* Large imbalance
* Small transfer limit

---

## Common Mistakes to Avoid

* Not dividing difference by 2
* Forgetting ceiling
* Using integer division incorrectly

---

## Interview Relevance

* Mathematical reasoning
* Greedy simplification
* Handling precision and rounding

---

## What This Problem Teaches

* Converting problems into formulas
* Using ceiling division
* Avoiding unnecessary simulation

---

## Key Takeaways

* Focus on balancing difference
* Use formula instead of loops
* Precision matters in division

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Arithmetic reasoning
* Optimization
* Clean implementation