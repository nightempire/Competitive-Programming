# A_Two_Elevators

## Platform

Codeforces

## Problem Link

[A. Two Elevators](https://codeforces.com/problemset/problem/1729/A)

## Problem Statement

There are **two elevators** in a building.

* **Elevator 1** is currently at floor `a`.
* **Elevator 2** is currently at floor `b`, but it must first go to floor `c` before it can reach floor `1`.

Your goal is to determine **which elevator reaches floor `1` faster**.

Rules:

* Elevator 1 goes directly from floor `a` to floor `1`.
* Elevator 2 first travels from floor `b` to floor `c`, then from floor `c` to floor `1`.

For each test case:

* Print `1` if **Elevator 1** reaches floor `1` faster.
* Print `2` if **Elevator 2** reaches floor `1` faster.
* Print `3` if **both elevators arrive at the same time**.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each test case consists of three integers:

```text
a b c
```

Where:

* `a` = starting floor of elevator 1
* `b` = starting floor of elevator 2
* `c` = floor elevator 2 must visit first

## Output Format

For each test case, print a single integer:

```
1
```

or

```
2
```

or

```
3
```

depending on which elevator is faster.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ a, b, c ≤ 100`

## Examples

### Example 1

Input

```
3
2 3 1
5 3 4
3 1 2
```

Explanation

Test Case 1

```
a = 2, b = 3, c = 1
```

Elevator 1 time:

```
|2 - 1| = 1
```

Elevator 2 time:

```
|3 - 1| + |1 - 1| = 2
```

Elevator 1 is faster.

Output

```
1
```

---

Test Case 2

```
a = 5, b = 3, c = 4
```

Elevator 1 time:

```
|5 - 1| = 4
```

Elevator 2 time:

```
|3 - 4| + |4 - 1| = 1 + 3 = 4
```

Both arrive at the same time.

Output

```
3
```

---

Test Case 3

```
a = 3, b = 1, c = 2
```

Elevator 1 time:

```
|3 - 1| = 2
```

Elevator 2 time:

```
|1 - 2| + |2 - 1| = 1 + 1 = 2
```

Both elevators take equal time.

Output

```
3
```

## Approach

Direct Distance Comparison

## Intuition

We simply calculate the **time required for each elevator to reach floor 1**.

Elevator 1 travels directly:

```
time1 = a - 1
```

Elevator 2 travels in two steps:

```
time2 = |b - c| + (c - 1)
```

Then compare the two times.

* If `time1 < time2` → Elevator 1 is faster
* If `time1 > time2` → Elevator 2 is faster
* If equal → Both arrive simultaneously

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read `a`, `b`, and `c`.
  * Compute:

```
first = a - 1
second = |b - c| + (c - 1)
```

* Compare `first` and `second`:

  * If `first < second` → print `1`
  * If `first > second` → print `2`
  * Otherwise → print `3`

## Visual Walkthrough

### Test Case 1

Input

```
a = 2
b = 3
c = 1
```

Elevator 1

```
2 → 1
time = 1
```

Elevator 2

```
3 → 1 → 1
time = 2
```

Result

```
Elevator 1 faster → Output = 1
```

---

### Test Case 2

Input

```
a = 5
b = 3
c = 4
```

Elevator 1

```
5 → 1
time = 4
```

Elevator 2

```
3 → 4 → 1
time = 1 + 3 = 4
```

Result

```
Equal → Output = 3
```

---

### Test Case 3

Input

```
a = 6
b = 2
c = 3
```

Elevator 1

```
6 → 1
time = 5
```

Elevator 2

```
2 → 3 → 1
time = 1 + 2 = 3
```

Result

```
Elevator 2 faster → Output = 2
```

## Complexity Analysis

### Time Complexity

```
O(t)
```

Each test case requires constant-time calculations.

### Space Complexity

```
O(1)
```

Only a few integer variables are used.

## Solution Explanation

The program calculates the travel time for both elevators.

* Elevator 1 moves directly to floor 1.
* Elevator 2 must first reach floor `c` and then go to floor `1`.

After computing both travel times, the program compares them and prints the appropriate result.

The implementation uses a **nested ternary operator** to simplify the comparison logic.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
#include<cmath>
using namespace std;

int main() {

    // Number of test cases
    int t, a, b, c;
    cin >> t;

    while(t--) {

        // Read floor positions
        cin >> a >> b >> c;

        // Time for elevator 1
        int first = a - 1;

        // Time for elevator 2
        int second = abs(b - c) + c - 1;

        // Compare times and print result
        cout << (first < second ? 1 : first > second ? 2 : 3) << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| a | b | c | Elevator 1 Time | Elevator 2 Time | Result |
| - | - | - | --------------- | --------------- | ------ |
| 2 | 3 | 1 | 1               | 2               | 1      |
| 5 | 3 | 4 | 4               | 4               | 3      |
| 6 | 2 | 3 | 5               | 3               | 2      |
| 4 | 4 | 4 | 3               | 3               | 3      |

## Edge Cases to Consider

* Both elevators already close to floor `1`
* `b = c`
* `c = 1`
* Equal travel times

## Common Test Cases

```
2 3 1
5 3 4
6 2 3
4 4 4
```

## Common Mistakes to Avoid

* Forgetting the second step for elevator 2 (`c → 1`)
* Using incorrect distance formulas
* Incorrect comparison logic

## Interview Relevance

* Tests understanding of distance calculations
* Demonstrates simple decision logic
* Reinforces conditional comparisons

## What This Problem Teaches

* Breaking down problems into smaller steps
* Comparing multiple scenarios efficiently
* Writing concise decision logic

## Key Takeaways

* Distance calculations are straightforward when broken into steps
* Always model the exact path before coding
* Ternary operators can simplify comparisons

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The task involves basic arithmetic and conditional comparisons, making it a straightforward implementation once the travel paths of the elevators are understood.