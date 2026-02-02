# A_Square

## Platform

Codeforces

## Problem Link

[A. Square?](https://codeforces.com/problemset/problem/1699/A)

## Problem Statement

You are given four integers `a`, `b`, `c`, and `d` for each test case.

Determine whether these four integers can represent the **four equal sides of a square**.

* If all four integers are **equal**, print `"YES"`.
* Otherwise, print `"NO"`.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * Four integers `a`, `b`, `c`, and `d` are provided on a single line.

## Output Format

* For each test case:

  * Print `"YES"` if all four numbers are equal.
  * Print `"NO"` otherwise.

Each answer must be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ a, b, c, d ≤ 1000`

## Examples

### Example 1

Input

```
3
1 1 1 1
2 2 2 3
5 5 5 5
```

Explanation

* Test case 1: All sides equal → valid square
* Test case 2: Last side differs → not a square
* Test case 3: All sides equal → valid square

Output

```
YES
NO
YES
```

---

### Example 2

Input

```
2
7 7 7 8
9 9 9 9
```

Output

```
NO
YES
```

## Approach

Simple equality comparison.

## Intuition

For four sides to form a square, all side lengths must be equal.
This translates to checking if:

```
a == b && b == c && c == d
```

If the above expression is true, then all four sides are equal.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read integers `a`, `b`, `c`, `d`
  * Compare all four values
  * If all equal, output `"YES"`
  * Otherwise, output `"NO"`

## Visual Walkthrough

### Case 1

```
Input:
3 3 3 3

All values equal → YES
```

### Case 2

```
Input:
4 4 5 4

One value differs → NO
```

## Complexity Analysis

### Time Complexity

**O(t)**
Each test case runs in constant time.

### Space Complexity

**O(1)**
Only a fixed number of variables are used.

## Solution Explanation

The solution reads four integers per test case and checks if they are all equal using simple comparison.
If the condition is satisfied, it prints `"YES"`; otherwise, it prints `"NO"`.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while(t--) {

        int a, b, c, d;
        cin >> a >> b >> c >> d;

        if(a == b && b == c && c == d)
            cout << "YES\n";
        else
            cout << "NO\n";
    }

    return 0;
}
```

## Test Cases Analysis

| Input Values | All Equal? | Output |
| ------------ | ---------- | ------ |
| `1 1 1 1`    | Yes        | YES    |
| `2 2 2 3`    | No         | NO     |
| `7 7 7 8`    | No         | NO     |
| `9 9 9 9`    | Yes        | YES    |

## Edge Cases to Consider

* All values the same
* Only one value differs
* Small constraint values

## Common Test Cases

* All sides equal
* One or more sides differ
* Random input combinations

## Common Mistakes to Avoid

* Using `||` instead of `&&` in comparisons
* Forgetting to read all input values per test case

## Interview Relevance

* Tests understanding of basic boolean logic
* Simple condition checks and repeated input handling

## What This Problem Teaches

* Counter checking for equality
* Reading and processing multiple test cases
* Translating a geometric property into code logic

## Key Takeaways

* Simple logic can answer geometric validation problems
* Use clear boolean comparisons for equality checks

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on simple equality checks and basic input/output handling, making it suitable for beginners in competitive programming.