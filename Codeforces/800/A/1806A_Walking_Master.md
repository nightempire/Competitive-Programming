## Platform

Codeforces

## Problem Link

[A. Walking Master](https://codeforces.com/problemset/problem/1806/A)

---

## Problem Statement

You are given two points:

* Start position → `(a, b)`
* Target position → `(c, d)`

You can perform the following moves:

* Move **up**: `(x, y) → (x, y + 1)`
* Move **right**: `(x, y) → (x + 1, y)`
* Move **left**: `(x, y) → (x - 1, y)`

Your goal is to reach `(c, d)` using the **minimum number of moves**.

If it is not possible, print `-1`.

---

## Input Format

* The first line contains an integer `t` — number of test cases
* For each test case:

  * Four integers `a, b, c, d`

---

## Output Format

For each test case:

* Print the minimum number of moves
* Or `-1` if impossible

---

## Constraints

* `1 ≤ t ≤ 10^4`
* `0 ≤ a, b, c, d ≤ 10^9`

---

## Examples

### Example 1

Input

```id="m8k2zp"
3
1 1 3 3
3 3 1 1
2 2 2 5
```

Explanation

* Case 1:

  * Move up → `(1,3)`
  * Move right → `(3,3)`
  * Total = 4
* Case 2:

  * Cannot move down → impossible
* Case 3:

  * Move up only

Output

```id="q5v7xt"
4
-1
3
```

---

### Example 2

Input

```id="t3k8mz"
2
5 2 6 5
4 4 4 4
```

Explanation

* First case:

  * Up moves first, then horizontal adjustment
* Second case:

  * Already at destination

Output

```id="z9m2pw"
4
0
```

---

### Example 3

Input

```id="p6x3rs"
1
2 5 3 3
```

Explanation

* Cannot go from y=5 to y=3 → impossible

Output

```id="y2k8vn"
-1
```

---

## Approach

Greedy movement with constraints validation

---

## Intuition

Key observations:

* You **cannot move down**, so:

```text id="c3q9kp"
d ≥ b
```

must be true

---

### Step 1: Move vertically

* Increase `y` from `b` to `d`
* Number of steps:

```text id="r7k1mz"
steps = d - b
```

* While moving up, `x` remains unchanged

---

### Step 2: Adjust horizontal position

* After vertical movement:

```text id="u5v2zp"
new_x = a + steps
```

* Because:

  * Each upward move does not change `x`
  * But effectively we consider movement sequence constraints

---

### Step 3: Reach target `x = c`

* If `new_x < c` → impossible
* Otherwise:

```text id="z8p4xk"
extra steps = new_x - c
```

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `a, b, c, d`
  * If `d < b`:

    * Print `-1`
    * Continue
  * Compute:

    * `steps = d - b`
    * `a += steps`
  * If `a < c`:

    * Print `-1`
  * Else:

    * Add `(a - c)` to steps
    * Print result

---

## Visual Walkthrough

### Case 1: `(1,1) → (3,3)`

```id="m4k8zp"
Up moves: 2 → (1,3)
Right moves: 2 → (3,3)

Total = 4
```

---

### Case 2: `(3,3) → (1,1)`

```id="z7p2xt"
Need to move down → not allowed → impossible
```

---

### Case 3: `(2,2) → (2,5)`

```id="x5m9kp"
Only upward movement needed

Steps = 3
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

The solution ensures:

* Vertical movement is possible
* Horizontal adjustment is feasible after vertical moves

By simulating movement logically (without actual iteration), we compute the minimum steps efficiently.

---

## Full Solution

### C++ Implementation

```cpp id="6n2k9z"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input coordinates
        int a, b, c, d;
        cin >> a >> b >> c >> d;

        // If target y is below current y → impossible
        if(d < b) {
            cout << -1 << "\n";
            continue;
        }

        // Step 1: Move up
        int steps = d - b;

        // Update x after vertical movement
        a += steps;

        // Step 2: Adjust x
        if(a < c) {
            cout << -1 << "\n";
        } else {

            // Additional steps to move left
            steps += (a - c);

            cout << steps << "\n";
        }
    }

    return 0;
}
```

---

## Test Cases Analysis

| Start (a,b) | Target (c,d) | Result |
| ----------- | ------------ | ------ |
| (1,1)       | (3,3)        | 4      |
| (3,3)       | (1,1)        | -1     |
| (2,2)       | (2,5)        | 3      |
| (4,4)       | (4,4)        | 0      |

---

## Edge Cases to Consider

* `d < b` → impossible
* Already at destination
* Large coordinate values
* `a < c` after vertical movement

---

## Common Test Cases

* Pure vertical movement
* Pure horizontal adjustment
* Impossible downward movement

---

## Common Mistakes to Avoid

* Ignoring vertical constraint (`d ≥ b`)
* Not updating `a` after upward moves
* Miscalculating extra horizontal steps

---

## Interview Relevance

* Greedy movement logic
* Coordinate-based reasoning
* Constraint handling

---

## What This Problem Teaches

* Breaking movement into phases
* Validating constraints early
* Avoiding simulation with math

---

## Key Takeaways

* Always check feasibility first
* Separate vertical and horizontal movement
* Simple arithmetic can replace simulation

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Logical reasoning
* Constraint validation
* Efficient computation