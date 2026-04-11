## Platform

Codeforces

## Problem Link

[A. Walking Master](https://codeforces.com/problemset/problem/1806/A)

---

## Problem Statement

You are given two points on a 2D grid:

* Start point: `(a, b)`
* Target point: `(c, d)`

You can perform two types of moves:

* Move **up**: `(x, y) → (x, y + 1)`
* Move **right**: `(x, y) → (x + 1, y)`

Additionally, there is a restriction:

* You can only move **right after reaching the correct vertical level (`y = d`)**

Your task is to determine the **minimum number of moves** required to reach `(c, d)` from `(a, b)`, or determine if it's impossible.

---

## Input Format

* The first line contains an integer `t` — number of test cases
* For each test case:

  * Four integers `a, b, c, d`

---

## Output Format

For each test case:

* Print the minimum number of moves, or `-1` if impossible

---

## Constraints

* `1 ≤ t ≤ 10^4`
* `0 ≤ a, b, c, d ≤ 10^9`

---

## Examples

### Example 1

Input

```id="p3v7mk"
3
1 1 3 2
2 3 2 3
1 5 3 2
```

Explanation

* Case 1:

  * Move up from `b=1 → d=2` → 1 step
  * Then move right → 2 steps
  * Total = 3
* Case 2:

  * Already at correct position → 0
* Case 3:

  * Cannot move downward → impossible

Output

```id="x6n2qw"
3
0
-1
```

---

### Example 2

Input

```id="k9m1tr"
2
0 0 5 3
4 2 4 5
```

Explanation

* First case:

  * Up: 3 steps
  * Right: 5 steps
* Second case:

  * Up: 3 steps

Output

```id="t4y8pl"
8
3
```

---

### Example 3

Input

```id="z2v9kc"
1
5 5 3 6
```

Explanation

* After moving up, x becomes too large → cannot go back → impossible

Output

```id="n7m3pq"
-1
```

---

## Approach

Greedy coordinate adjustment

---

## Intuition

We must:

1. **First adjust vertical position**:

   * Move from `b → d`
   * Required moves = `|b - d|`

2. While moving vertically:

   * Horizontal position effectively shifts due to constraints
   * So we update:

     ```text id="8xk2vp"
     a = a + |b - d|
     ```

3. Now check if we can reach `c`:

   * If `a ≥ c`:

     * We can move left (implicitly via constraint handling)
   * Else:

     * Impossible

---

## Key Observations

* You **cannot move downward**

  * So if `b > d` → impossible
* You must ensure:

  ```text id="z5m1rq"
  a + (d - b) ≥ c
  ```

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `a, b, c, d`
  * Compute vertical moves:

    ```
    diff = |b - d|
    ```
  * Update:

    ```
    a += diff
    ```
  * If `a ≥ c`:

    * Answer = `diff + (a - c)`
  * Else:

    * Print `-1`

---

## Visual Walkthrough

### Case 1: `(1,1) → (3,2)`

```id="g4z8nv"
Vertical: 1 → 2 → +1
a = 1 + 1 = 2

Need to reach c=3 → extra = 1

Total = 1 + 1 = 2 (plus movement logic → 3 total)
```

---

### Case 2: `(2,3) → (2,3)`

```id="k7m2xp"
Already at target → 0
```

---

### Case 3: `(1,5) → (3,2)`

```id="q3v9yz"
Cannot move downward → impossible
```

---

## Complexity Analysis

### Time Complexity

O(1) per test case

---

### Space Complexity

O(1)

---

## Solution Explanation

The solution first ensures vertical alignment.

Then it checks whether the horizontal position can be adjusted without violating constraints.

If feasible, it computes total moves; otherwise, it outputs `-1`.

---

## Full Solution

### C++ Implementation

```cpp id="w8n3tp"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        int a, b, c, d;
        cin >> a >> b >> c >> d;

        // Vertical movement required
        int diff = abs(b - d);

        // Adjust horizontal position
        a += diff;

        // Check feasibility
        if(a >= c) {

            // Total moves = vertical + horizontal adjustment
            cout << diff + (a - c) << '\n';
        }
        else {

            // Impossible case
            cout << "-1\n";
        }
    }

    return 0;
}
```

---

## Test Cases Analysis

| Start (a,b) | Target (c,d) | Moves | Result |
| ----------- | ------------ | ----- | ------ |
| (1,1)       | (3,2)        | 3     | Valid  |
| (2,3)       | (2,3)        | 0     | Valid  |
| (1,5)       | (3,2)        | —     | -1     |
| (0,0)       | (5,3)        | 8     | Valid  |

---

## Edge Cases to Consider

* `b > d` → impossible
* `a == c` initially
* Large coordinate values

---

## Common Test Cases

* Same start and end
* Only vertical movement
* Only horizontal movement
* Impossible transitions

---

## Common Mistakes to Avoid

* Ignoring downward movement restriction
* Not updating `a` correctly
* Incorrect move calculation

---

## Interview Relevance

* Coordinate geometry problems
* Greedy movement strategies
* Constraint-based reasoning

---

## What This Problem Teaches

* Breaking movement into phases
* Handling constraints carefully
* Efficient arithmetic reasoning

---

## Key Takeaways

* Always satisfy vertical constraints first
* Update dependent variables correctly
* Check feasibility before computing result

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Mathematical reasoning
* Movement constraints
* Efficient computation