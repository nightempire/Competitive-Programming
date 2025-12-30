# A. Buy a Shovel

## Platform

Codeforces

## Problem Link

[A. Buy a Shovel](https://codeforces.com/problemset/problem/732/A)

## Problem Statement

Polycarp wants to buy some shovels.
Each shovel costs `k` burles.

He wants to buy an integer number of shovels such that the **total cost**:

* Ends with digit `0`, or
* Ends with digit `r`

Given the values of `k` and `r`, determine the **minimum number of shovels** Polycarp must buy to satisfy this condition.

## Input Format

A single line containing two integers:

```
k r
```

## Output Format

Print a single integer representing the minimum number of shovels to buy.

## Constraints

* `1 ≤ k ≤ 1000`
* `0 ≤ r ≤ 9`

## Examples

### Example 1

Input

```
117 3
```

Explanation

Multiples of `117`:

```
117 → ends with 7
234 → ends with 4
351 → ends with 1
468 → ends with 8
585 → ends with 5
702 → ends with 2
819 → ends with 9
936 → ends with 6
1053 → ends with 3
```

The first multiple ending with `3` occurs at `9`.

Output

```
9
```

### Example 2

Input

```
10 5
```

Explanation
`10 × 1 = 10` ends with `0`.

Output

```
1
```

### Example 3

Input

```
7 0
```

Explanation
`7 × 10 = 70` ends with `0`.

Output

```
10
```

## Approach

**Brute-Force Iteration Over Small Range**

## Intuition

Only the **last digit** of the total cost matters.

By checking successive multiples of `k`, we can determine when the last digit becomes either `0` or `r`.
Since digits repeat every `10`, checking up to `9` multiples is sufficient.

## Algorithm Steps

* Read values `k` and `r`
* Iterate `i` from `1` to `9`
* Compute `(i × k) % 10`
* If the result is `0` or equals `r`:

  * Output `i`
  * Stop execution

## Visual Walkthrough

Input:

```
k = 117, r = 3
```

Check multiples:

```
1 × 117 → 7
2 × 117 → 4
3 × 117 → 1
...
9 × 117 → 3  ✔
```

Minimum number of shovels:

```
9
```

Another case:

```
k = 10, r = 5
1 × 10 → 0 ✔
```

## Complexity Analysis

### Time Complexity

O(1)

The loop runs at most 9 iterations, which is constant time.

### Space Complexity

O(1)

Only constant extra variables are used.

## Solution Explanation

The solution leverages the cyclic nature of the last digit of multiples.
By checking small successive multiples of `k`, it quickly finds the smallest multiplier that produces a total cost ending in either `0` or the required digit `r`.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // k -> cost of one shovel
    // r -> required last digit
    int k, r;
    cin >> k >> r;

    // Try buying 1 to 9 shovels
    for (int i = 1; i <= 9; i++) {

        // Calculate the last digit of total cost
        int rem = (i * k) % 10;

        // If last digit is 0 or matches r,
        // this is the minimum valid number of shovels
        if (rem == 0 || rem == r) {
            cout << i << '\n';
            return 0;
        }
    }

    return 0;
}
```

## Test Cases Analysis

| k   | r | Result |
| --- | - | ------ |
| 117 | 3 | 9      |
| 10  | 5 | 1      |
| 7   | 0 | 10     |
| 1   | 1 | 1      |

## Edge Cases to Consider

* `k` already ends with `0`
* `r = 0`
* Smallest possible values of `k`

## Common Test Cases

* Direct match on first multiplication
* Match after several iterations
* Match only when last digit becomes zero

## Common Mistakes to Avoid

* Iterating unnecessarily beyond 9
* Comparing full value instead of last digit
* Forgetting modulo operation

## Interview Relevance

* Tests understanding of modular arithmetic
* Demonstrates pattern recognition
* Evaluates optimization through constraints

## What This Problem Teaches

* Importance of modular arithmetic
* Efficient brute-force within constraints
* Leveraging digit patterns in numbers

## Key Takeaways

* Last digit behavior repeats every 10
* Small brute-force loops can be optimal
* Constraints often guide efficient solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes arithmetic reasoning and constraint-based optimization, making it suitable for beginners and early interview practice.