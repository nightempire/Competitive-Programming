# B. Journey

## Platform

Codeforces

## Problem Link

[B. Journey - Codeforces Problem 2051B](https://codeforces.com/problemset/problem/2051/B?utm_source=chatgpt.com)

## Problem Statement

A traveler follows a repeating 3-day journey pattern:

* Day 1: travels `a` kilometers
* Day 2: travels `b` kilometers
* Day 3: travels `c` kilometers

After Day 3, the pattern repeats again starting from Day 1.

Given the total distance `n` that must be covered, determine the minimum number of days required to travel at least `n` kilometers.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * A single line contains four integers:

```text
n a b c
```

where:

* `n` = required distance
* `a` = distance traveled on Day 1
* `b` = distance traveled on Day 2
* `c` = distance traveled on Day 3

## Output Format

For each test case, print a single integer — the minimum number of days required to travel at least `n` kilometers.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 10^9`
* `1 ≤ a, b, c ≤ 10^9`

## Examples

### Example 1

Input

```text
1
12 2 3 4
```

Output

```text
5
```

### Explanation

One complete cycle:

```text
Day 1 → 2 km
Day 2 → 3 km
Day 3 → 4 km
```

Total per cycle:

```text
2 + 3 + 4 = 9 km
```

After 3 days:

```text
9 km
```

Remaining distance:

```text
12 - 9 = 3 km
```

Day 4:

```text
+2 km → 11 km
```

Day 5:

```text
+3 km → 14 km
```

Distance requirement is reached on Day 5.

---

### Example 2

Input

```text
1
10 5 4 3
```

Output

```text
3
```

### Explanation

Journey progression:

```text
Day 1 → 5 km
Day 2 → 9 km
Day 3 → 12 km
```

Required distance is reached on Day 3.

---

### Example 3

Input

```text
1
7 8 2 1
```

Output

```text
1
```

### Explanation

Day 1 alone covers:

```text
8 km
```

Since:

```text
8 ≥ 7
```

Only one day is needed.

## Approach

### Algorithm Type

Mathematical Simulation using Complete Cycles

## Intuition

The journey repeats every 3 days.

Let:

```text
cycleDistance = a + b + c
```

Every complete cycle contributes exactly:

```text
3 days
```

and covers:

```text
a + b + c kilometers
```

Therefore:

1. Calculate how many complete cycles fit into `n`.
2. Count the corresponding days.
3. Handle the remaining distance using the next partial cycle.

This avoids simulating day-by-day travel for very large values.

## Algorithm Steps

* Read `t`.
* For each test case:

  * Read `n`, `a`, `b`, and `c`.
  * Compute:

```text
sum = a + b + c
```

* Compute complete cycles:

```text
cycles = n / sum
```

* Add:

```text
cycles × 3
```

days to the answer.

* Compute remaining distance:

```text
rem = n % sum
```

* If `rem = 0`:

  * Answer is already complete.
* Otherwise:

  * If `rem ≤ a`, add 1 day.
  * Else if `rem ≤ a + b`, add 2 days.
  * Else add 3 days.
* Print the result.

## Visual Walkthrough

### Test Case 1

Input:

```text
n = 12
a = 2
b = 3
c = 4
```

Cycle distance:

```text
2 + 3 + 4 = 9
```

Complete cycles:

```text
12 / 9 = 1
```

Days so far:

```text
1 × 3 = 3
```

Remaining:

```text
12 % 9 = 3
```

Partial cycle:

```text
Day 4 → +2
Remaining still needed
```

```text
Day 5 → +3
Reached target
```

Answer:

```text
5
```

---

### Test Case 2

Input:

```text
n = 20
a = 3
b = 4
c = 5
```

Cycle distance:

```text
12
```

Complete cycles:

```text
20 / 12 = 1
```

Days:

```text
3
```

Remaining:

```text
8
```

Check:

```text
8 > 3
8 > 3+4
8 ≤ 3+4+5
```

Need all three days of the next cycle.

Answer:

```text
6
```

---

### Test Case 3

Input:

```text
n = 25
a = 10
b = 3
c = 2
```

Cycle distance:

```text
15
```

Complete cycles:

```text
25 / 15 = 1
```

Days:

```text
3
```

Remaining:

```text
10
```

Since:

```text
10 ≤ a
```

Only one additional day is required.

Answer:

```text
4
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case.

Only a few arithmetic operations are performed:

* Addition
* Division
* Modulo
* Comparisons

Therefore:

```text
O(1)
```

For all test cases:

```text
O(t)
```

---

### Space Complexity

**O(1)**

Only a fixed number of variables are used.

No extra data structures are required.

## Solution Explanation

The journey repeats in blocks of three days.

Instead of simulating every day, the solution first determines how many complete 3-day cycles can be used.

Each complete cycle contributes:

```text
a + b + c
```

distance and:

```text
3
```

days.

After accounting for all complete cycles, only a small remainder remains.

The remainder can always be covered within at most three additional days:

* Day 1 contributes `a`
* Days 1+2 contribute `a+b`
* Days 1+2+3 contribute `a+b+c`

Checking these three possibilities yields the minimum number of extra days.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Required distance and daily distances
        int n, a, b, c;
        cin >> n >> a >> b >> c;

        // Distance covered in one complete 3-day cycle
        int sum = a + b + c;

        // Days contributed by complete cycles
        int days = (n / sum) * 3;

        // Remaining distance after complete cycles
        int rem = n % sum;

        // Handle the remaining distance
        if(rem != 0) {

            // Reach target on Day 1 of next cycle
            if(rem <= a) {
                days += 1;
            }

            // Reach target on Day 2 of next cycle
            else if(rem <= a + b) {
                days += 2;
            }

            // Reach target on Day 3 of next cycle
            else {
                days += 3;
            }
        }

        // Print minimum days required
        cout << days << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n  | a  | b | c | Cycle Distance | Days Required |
| -- | -- | - | - | -------------- | ------------- |
| 12 | 2  | 3 | 4 | 9              | 5             |
| 10 | 5  | 4 | 3 | 12             | 3             |
| 7  | 8  | 2 | 1 | 11             | 1             |
| 20 | 3  | 4 | 5 | 12             | 6             |
| 25 | 10 | 3 | 2 | 15             | 4             |

## Edge Cases to Consider

* `n` is exactly equal to one cycle distance.
* `n` is smaller than `a`.
* Remainder is exactly `a`.
* Remainder is exactly `a + b`.
* Very large values of `n`.
* Only one additional day is needed after complete cycles.

## Common Test Cases

### Distance Reached on First Day

```text
Input:
1
5 10 2 1

Output:
1
```

---

### Exact Cycle Completion

```text
Input:
1
12 3 4 5

Output:
3
```

---

### Need Two Extra Days

```text
Input:
1
15 4 5 3

Output:
5
```

---

### Need Three Extra Days

```text
Input:
1
20 3 4 5

Output:
6
```

## Common Mistakes to Avoid

* Forgetting to handle the case when `rem = 0`.
* Simulating day-by-day instead of using cycle mathematics.
* Using incorrect conditions for determining whether 1, 2, or 3 extra days are needed.

## Interview Relevance

* Demonstrates cycle-based optimization.
* Tests mathematical reasoning and modular arithmetic.
* Shows how repetitive processes can be compressed into constant-time calculations.

## What This Problem Teaches

* Identifying repeating patterns.
* Using division and modulo to process cycles efficiently.
* Replacing simulation with mathematical analysis.

## Key Takeaways

* Repeating processes often have a cycle that can be exploited.
* Complete cycles can be handled using division.
* Remaining work is typically handled using modulo arithmetic.
* Mathematical solutions can reduce linear simulations to constant time.

## Problem Difficulty Analysis

This is an **Easy** mathematics and implementation problem.

The main observation is that the travel pattern repeats every three days. Once the repeating cycle is identified, the solution becomes a straightforward application of division, modulo arithmetic, and a few conditional checks, resulting in an efficient **O(1)** solution per test case.