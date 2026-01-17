# A_Maximum_GCD

## Platform

Codeforces

## Problem Link

[A. Maximum GCD](https://codeforces.com/problemset/problem/1758/A)

## Problem Statement

You are given an integer `n`.

Your task is to choose **two distinct positive integers** `a` and `b` such that:

* `1 ≤ a < b ≤ n`
* The **Greatest Common Divisor (GCD)** of `a` and `b` is **maximized**

For each test case, output the **maximum possible GCD**.

Each test case is independent.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * A single integer `n`.

## Output Format

* For each test case, print a single integer representing the **maximum possible GCD**.

## Constraints

* `1 ≤ t ≤ 1000`
* `2 ≤ n ≤ 10⁹`

## Examples

### Example 1

Input

```
3
2
5
10
```

Explanation

* `n = 2`
  Only possible pair: `(1, 2)` → `gcd = 1`

* `n = 5`
  Best pair: `(2, 4)` → `gcd = 2`

* `n = 10`
  Best pair: `(5, 10)` → `gcd = 5`

Output

```
1
2
5
```

---

### Example 2

Input

```
1
7
```

Explanation

* Best pair: `(3, 6)` → `gcd = 3`

Output

```
3
```

## Approach

**Mathematical Observation**

## Intuition

To maximize the GCD of two numbers:

* Both numbers should be **multiples of the same large number**
* The largest possible common divisor for numbers ≤ `n` is achieved by:

  ```
  a = k
  b = 2k
  ```

  where `2k ≤ n`

The largest such `k` is:

```
k = ⌊n / 2⌋
```

Thus, the maximum GCD is simply `n / 2`.

## Algorithm Steps

* Read number of test cases `t`.
* For each test case:

  * Read integer `n`.
  * Output `n / 2`.

## Visual Walkthrough

### Test Case: `n = 10`

Possible optimal pair:

```
a = 5
b = 10
```

GCD:

```
gcd(5, 10) = 5
```

Result:

```
n / 2 = 5
```

---

### Test Case: `n = 7`

Possible optimal pair:

```
a = 3
b = 6
```

GCD:

```
gcd(3, 6) = 3
```

Result:

```
n / 2 = 3
```

## Complexity Analysis

### Time Complexity

**O(1) per test case**

* Only a constant-time division operation.

### Space Complexity

**O(1)**

* No additional memory used.

## Solution Explanation

The solution relies on a key mathematical insight:
the maximum GCD of any two numbers not exceeding `n` is obtained by choosing two numbers where one is exactly twice the other.

By selecting the largest such possible value (`n / 2`), we guarantee the maximum GCD.

This leads to an extremely concise and optimal solution.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while (t--) {

        int n;
        cin >> n;

        // Maximum possible GCD
        cout << n / 2 << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n  | Best Pair | Maximum GCD |
| -- | --------- | ----------- |
| 2  | (1, 2)    | 1           |
| 3  | (1, 2)    | 1           |
| 5  | (2, 4)    | 2           |
| 7  | (3, 6)    | 3           |
| 10 | (5, 10)   | 5           |

## Edge Cases to Consider

* Minimum valid value (`n = 2`)
* Odd values of `n`
* Very large values of `n`

## Common Test Cases

* Small values of `n`
* Large values of `n`
* Multiple test cases

## Common Mistakes to Avoid

* Trying unnecessary GCD computations
* Overthinking pair selection
* Using brute-force approaches

## Interview Relevance

* Tests mathematical reasoning
* Evaluates ability to simplify problems
* Common example of observation-based optimization

## What This Problem Teaches

* Importance of identifying patterns
* Leveraging mathematical properties
* Writing optimal constant-time solutions

## Key Takeaways

* Maximum GCD depends only on `n`
* Simple division solves the problem
* Observation beats brute force

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses entirely on mathematical insight rather than implementation complexity.