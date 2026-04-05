## Platform

Codeforces

## Problem Link

[A. Free Ice Cream](https://codeforces.com/problemset/problem/686/A)

---

## Problem Statement

Dima has an ice cream shop.

Initially, he has `x` ice cream packs. Then `n` events occur.

Each event is one of the following:

* `'+' d` → Add `d` ice creams
* `'-' d` → Give `d` ice creams to a customer

However, if Dima does not have enough ice creams to fulfill a request:

* The request is **denied**
* A counter of **distressed kids** increases

Your task is to determine:

* The final number of ice creams
* The number of distressed kids

---

## Input Format

* First line: two integers `n` and `x`
* Next `n` lines:

  * Each line contains:

    * A character `op` (`'+'` or `'-'`)
    * An integer `d`

---

## Output Format

* Print two integers:

  * Final ice creams
  * Number of distressed kids

---

## Constraints

* `1 ≤ n ≤ 1000`
* `0 ≤ x ≤ 10^9`
* `1 ≤ d ≤ 10^9`

---

## Examples

### Example 1

Input

```id="k3n9t2"
4 10
+ 5
- 3
- 20
+ 10
```

Explanation

* Start: `x = 10`
* `+5` → `15`
* `-3` → `12`
* `-20` → not enough → distressed = 1
* `+10` → `22`

Output

```id="g7x2qp"
22 1
```

---

### Example 2

Input

```id="t2d8kq"
3 5
- 2
- 3
- 1
```

Explanation

* `-2` → `3`
* `-3` → `0`
* `-1` → not enough → distressed = 1

Output

```id="u8z5ml"
0 1
```

---

### Example 3

Input

```id="r9m1zp"
2 0
+ 10
- 5
```

Explanation

* `+10` → `10`
* `-5` → `5`

Output

```id="v4q7yb"
5 0
```

---

## Approach

Simulation with conditional checks

---

## Intuition

We simulate each operation:

* If adding → increase total
* If removing:

  * Check if enough ice cream exists
  * If yes → subtract
  * If no → increment distressed counter

---

## Algorithm Steps

* Read `n` and `x`
* Initialize `count = 0` (distressed kids)
* For each of `n` operations:

  * Read `op` and `d`
  * If `op == '+'`:

    * `x += d`
  * Else:

    * If `x < d`:

      * `count++`
    * Else:

      * `x -= d`
* Print `x` and `count`

---

## Visual Walkthrough

### Case 1

```id="a6p3k9"
Start = 10

+5  → 15
-3  → 12
-20 → not enough → count = 1
+10 → 22
```

---

### Case 2

```id="p2x8mv"
Start = 5

-2 → 3
-3 → 0
-1 → not enough → count = 1
```

---

### Case 3

```id="m4k9zt"
Start = 0

+10 → 10
-5  → 5
```

---

## Complexity Analysis

### Time Complexity

O(n)

* Each operation processed once

---

### Space Complexity

O(1)

* Only variables used

---

## Solution Explanation

The problem is a direct simulation.

We maintain:

* Current ice cream count
* Distressed kids counter

Each operation is processed sequentially, ensuring correctness and efficiency.

---

## Full Solution

### C++ Implementation

```cpp id="x3p7nv"
#include<iostream>
using namespace std;

int main() {

    // Number of operations and initial ice creams
    int n, count = 0;
    long long x;

    cin >> n >> x;

    // Process each operation
    while(n--) {

        char op;
        long long d;

        cin >> op >> d;

        // Addition operation
        if(op == '+') {
            x += d;
        }

        // Subtraction operation
        else {

            // Not enough ice creams
            if(x < d) {
                count++;
            }
            else {
                x -= d;
            }
        }
    }

    // Output final ice creams and distressed kids
    cout << x << ' ' << count;

    return 0;
}
```

---

## Test Cases Analysis

| Initial x | Operations       | Final x | Distressed |
| --------- | ---------------- | ------- | ---------- |
| 10        | +5, -3, -20, +10 | 22      | 1          |
| 5         | -2, -3, -1       | 0       | 1          |
| 0         | +10, -5          | 5       | 0          |

---

## Edge Cases to Consider

* Initial `x = 0`
* Large values of `d`
* All operations are subtraction
* No distressed cases

---

## Common Test Cases

* Only additions
* Only subtractions
* Mixed operations
* Multiple failures

---

## Common Mistakes to Avoid

* Subtracting even when insufficient stock
* Not counting failed operations
* Using incorrect data types (use `long long`)

---

## Interview Relevance

* Simulation problems
* Conditional logic handling
* State tracking

---

## What This Problem Teaches

* Efficient simulation of operations
* Importance of condition checking
* Handling large numbers safely

---

## Key Takeaways

* Always validate before subtracting
* Use proper data types for large values
* Simple simulations can solve many problems

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Simulation
* Conditional checks
* Basic input/output handling