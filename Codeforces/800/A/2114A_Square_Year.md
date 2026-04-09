## Platform

Codeforces

## Problem Link

[A. Square Year](https://codeforces.com/problemset/problem/2114/A)

---

## Problem Statement

You are given an integer `year`.

Your task is to determine whether `year` can be expressed in the form:

```text
(a + b)² = year
```

where:

* `a` and `b` are **non-negative integers**

If possible:

* Output any valid pair `(a, b)`

Otherwise:

* Output `-1`

---

## Input Format

* The first line contains an integer `t` — number of test cases
* Each test case contains a single integer `year`

---

## Output Format

For each test case:

* Print two integers `a b` such that `(a + b)² = year`
* Or print `-1` if not possible

---

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ year ≤ 10^9`

---

## Examples

### Example 1

Input

```id="z4m2qk"
3
1
4
5
```

Explanation

* `1 = (1 + 0)²`
* `4 = (2 + 0)²`
* `5` is not a perfect square

Output

```id="x9p3vl"
1 0
2 0
-1
```

---

### Example 2

Input

```id="k6n7zd"
2
9
10
```

Explanation

* `9 = (3 + 0)²`
* `10` is not a perfect square

Output

```id="t2m5rs"
3 0
-1
```

---

### Example 3

Input

```id="v8q1xp"
1
16
```

Explanation

* `16 = (4 + 0)²`

Output

```id="u5z3nw"
4 0
```

---

## Approach

Perfect square check using square root

---

## Intuition

The equation:

```text
(a + b)² = year
```

implies:

```text
a + b = √year
```

So:

* If `year` is a **perfect square**, then a solution exists
* Otherwise, it is impossible

We can simply choose:

```text
a = √year, b = 0
```

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `year`
  * Compute `a = floor(sqrt(year))`
  * If `a * a == year`:

    * Print `a 0`
  * Else:

    * Print `-1`

---

## Visual Walkthrough

### Case 1: `year = 9`

```id="g3r8zn"
√9 = 3

3² = 9 → valid

Output: 3 0
```

---

### Case 2: `year = 10`

```id="p4m6yk"
√10 ≈ 3.16

3² = 9 ≠ 10 → invalid
```

---

### Case 3: `year = 16`

```id="n2k5xp"
√16 = 4

4² = 16 → valid
```

---

## Complexity Analysis

### Time Complexity

O(1) per test case

* Constant-time square root calculation

---

### Space Complexity

O(1)

* No extra space used

---

## Solution Explanation

The solution checks whether the given number is a perfect square.

If yes:

* The equation `(a + b)² = year` can be satisfied
* A valid solution is `(a, b) = (√year, 0)`

Otherwise:

* No such integers exist

---

## Full Solution

### C++ Implementation

```cpp id="p8v3qk"
#include<iostream>
#include<cmath>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input year
        int year;
        cin >> year;

        // Compute integer square root
        int a = sqrt(year);

        // Check if perfect square
        if(a * a == year) {

            // Valid case
            cout << a << " 0\n";
        }
        else {

            // Not a perfect square
            cout << "-1\n";
        }
    }

    return 0;
}
```

---

## Test Cases Analysis

| year | √year | Perfect Square | Output |
| ---- | ----- | -------------- | ------ |
| 1    | 1     | Yes            | 1 0    |
| 4    | 2     | Yes            | 2 0    |
| 5    | 2     | No             | -1     |
| 9    | 3     | Yes            | 3 0    |
| 10   | 3     | No             | -1     |

---

## Edge Cases to Consider

* `year = 1`
* Large perfect squares (e.g., `10^9`)
* Non-perfect squares

---

## Common Test Cases

* Perfect square values
* Non-perfect square values
* Boundary values

---

## Common Mistakes to Avoid

* Using floating-point comparison incorrectly
* Not verifying `a * a == year`
* Relying only on `sqrt` without validation

---

## Interview Relevance

* Mathematical reasoning
* Square root usage
* Edge case handling

---

## What This Problem Teaches

* Identifying perfect square patterns
* Efficient validation techniques
* Avoiding floating-point pitfalls

---

## Key Takeaways

* Always verify square root results
* Perfect square problems are common
* Simple math can simplify logic

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Basic mathematics
* Conditional logic
* Efficient checking