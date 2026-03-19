# C_Hard_Problem

## Platform

Codeforces

## Problem Link

[C. Hard Problem](https://codeforces.com/problemset/problem/2044/C)

## Problem Statement

You are organizing a contest with **two groups**, each having capacity `m`.

There are three types of participants:

* `a` participants who prefer **group 1**
* `b` participants who prefer **group 2**
* `c` participants who have **no preference**

Each group can contain at most `m` participants.

Your goal is to maximize the **total number of participants assigned** to the two groups.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each test case contains four integers:

```text
m a b c
```

## Output Format

For each test case, print a single integer — the **maximum number of participants that can be assigned**.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ m ≤ 10^9`
* `0 ≤ a, b, c ≤ 10^9`

## Examples

### Example 1

Input

```
3
5 3 4 2
3 5 5 5
2 1 1 10
```

Explanation

Test Case 1

```
m = 5, a = 3, b = 4, c = 2
```

Assign preferred participants:

```
Group 1: min(5,3) = 3
Group 2: min(5,4) = 4
```

Used:

```
3 + 4 = 7
```

Remaining capacity:

```
2*5 - 7 = 3
```

Use `c`:

```
min(2,3) = 2
```

Total:

```
7 + 2 = 9
```

Output

```
9
```

---

### Example 2

Input

```
1
3 5 5 5
```

Explanation

Preferred:

```
3 + 3 = 6
```

Remaining:

```
6 - 6 = 0
```

Total:

```
6
```

Output

```
6
```

---

### Example 3

Input

```
1
2 1 1 10
```

Explanation

Preferred:

```
1 + 1 = 2
```

Remaining:

```
4 - 2 = 2
```

Use `c`:

```
min(10,2) = 2
```

Total:

```
4
```

Output

```
4
```

## Approach

Greedy Allocation with Capacity Constraints

## Intuition

We prioritize assigning participants who have **fixed preferences**:

* Fill group 1 with `a`
* Fill group 2 with `b`

But each group can hold at most `m`.

So:

```
group1_used = min(m, a)
group2_used = min(m, b)
```

Then calculate remaining capacity:

```
remaining = 2*m - (group1_used + group2_used)
```

Now fill remaining slots using flexible participants `c`.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read `m`, `a`, `b`, `c`.
  * Compute:

```
used = min(m, a) + min(m, b)
```

* Compute remaining capacity:

```
rem = 2*m - used
```

* Add flexible participants:

```
result = used + min(c, rem)
```

* Print result.

## Visual Walkthrough

### Test Case 1

Input

```
m = 5, a = 3, b = 4, c = 2
```

Step 1 — Assign preferred:

```
Group 1 → 3
Group 2 → 4
```

Step 2 — Remaining:

```
10 - 7 = 3
```

Step 3 — Fill with `c`:

```
min(2,3) = 2
```

Total:

```
9
```

---

### Test Case 2

```
m = 3, a = 5, b = 5, c = 5
```

Preferred:

```
3 + 3 = 6
```

Remaining:

```
6 - 6 = 0
```

Total:

```
6
```

---

### Test Case 3

```
m = 2, a = 1, b = 1, c = 10
```

Preferred:

```
1 + 1 = 2
```

Remaining:

```
4 - 2 = 2
```

Fill:

```
min(10,2) = 2
```

Total:

```
4
```

## Complexity Analysis

### Time Complexity

```
O(t)
```

Each test case uses constant time operations.

### Space Complexity

```
O(1)
```

Only a few variables are used.

## Solution Explanation

The solution follows a **greedy approach**:

1. First assign participants with fixed preferences.
2. Then fill remaining capacity with flexible participants.

This ensures:

* Maximum utilization of both groups
* No violation of capacity constraints

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    int t, m, a, b, c;
    cin >> t;

    while(t--) {

        cin >> m >> a >> b >> c;

        // Assign preferred participants
        int used = min(m, a) + min(m, b);

        // Remaining capacity
        int rem = 2 * m - used;

        // Fill with flexible participants
        int result = used + min(c, rem);

        cout << result << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| m | a | b | c  | Used | Remaining | Result |
| - | - | - | -- | ---- | --------- | ------ |
| 5 | 3 | 4 | 2  | 7    | 3         | 9      |
| 3 | 5 | 5 | 5  | 6    | 0         | 6      |
| 2 | 1 | 1 | 10 | 2    | 2         | 4      |

## Edge Cases to Consider

* `a` or `b` exceeds `m`
* `c = 0`
* All values are zero
* Very large inputs

## Common Test Cases

```
5 3 4 2
3 5 5 5
2 1 1 10
1 0 0 0
```

## Common Mistakes to Avoid

* Not capping `a` and `b` with `m`
* Forgetting to calculate remaining capacity
* Overfilling beyond `2*m`

## Interview Relevance

* Demonstrates greedy allocation
* Shows capacity constraint handling
* Tests arithmetic reasoning

## What This Problem Teaches

* Efficient resource allocation
* Greedy strategies under constraints
* Breaking problems into stages

## Key Takeaways

* Always prioritize constrained assignments first
* Fill remaining capacity with flexible elements
* Greedy strategies often yield optimal solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It primarily involves understanding capacity constraints and applying a simple greedy strategy to maximize utilization.