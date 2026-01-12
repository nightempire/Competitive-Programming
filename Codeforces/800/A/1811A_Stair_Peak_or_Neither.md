# A_Stair_Peak_or_Neither

## Platform

Codeforces

## Problem Link

[A. Stair, Peak, or Neither](https://codeforces.com/problemset/problem/1811/A)

## Problem Statement

You are given three integers `a`, `b`, and `c` for each test case.

Based on their relative values, determine whether the sequence forms:

* **STAIR** → strictly increasing order
  `a < b < c`

* **PEAK** → middle value is strictly greater than both ends
  `a < b > c`

* **NONE** → any other arrangement

For each test case, print the appropriate classification.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case consists of one line containing three integers `a`, `b`, and `c`.

## Output Format

For each test case, print one of the following strings:

* `STAIR`
* `PEAK`
* `NONE`

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `0 ≤ a, b, c ≤ 100`

## Examples

### Example 1

Input

```
3
1 2 3
1 3 2
2 1 3
```

Explanation

* Test case 1
  `1 < 2 < 3` → STAIR

* Test case 2
  `1 < 3 > 2` → PEAK

* Test case 3
  No valid increasing or peak pattern → NONE

Output

```
STAIR
PEAK
NONE
```

### Example 2

Input

```
1
5 5 5
```

Explanation
All values are equal, so neither condition is satisfied.

Output

```
NONE
```

## Approach (Algorithm Name / Type)

**Conditional Pattern Classification**

## Intuition

Only the **relative ordering** of the three values matters.

By checking two simple conditions in order:

* strictly increasing
* peak-shaped

we can classify every possible input combination correctly.
Any case that does not match these patterns must be labeled as `NONE`.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read integers `a`, `b`, and `c`
  * If `a < b` and `b < c`, print `STAIR`
  * Else if `a < b` and `b > c`, print `PEAK`
  * Otherwise, print `NONE`

## Visual Walkthrough

### Test Case 1

Input

```
a = 1, b = 2, c = 3
```

Comparison

```
1 < 2 < 3
```

Result

```
STAIR
```

---

### Test Case 2

Input

```
a = 1, b = 3, c = 2
```

Comparison

```
1 < 3 > 2
```

Result

```
PEAK
```

---

### Test Case 3

Input

```
a = 2, b = 1, c = 3
```

Comparison
No valid pattern

Result

```
NONE
```

## Complexity Analysis

### Time Complexity

**O(t)**
Each test case is processed using constant-time comparisons.

### Space Complexity

**O(1)**
No additional memory is used beyond simple variables.

## Solution Explanation

The solution relies entirely on conditional comparisons between the three integers.
Since only two valid patterns exist, the logic is minimal, efficient, and easy to verify.

By checking the **STAIR** condition first, ambiguity is avoided, and correctness is guaranteed.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Read the three integers
        int a, b, c;
        cin >> a >> b >> c;

        // Check for strictly increasing order
        if (a < b && b < c) {

            // a < b < c forms a stair pattern
            cout << "STAIR\n";
        }
        // Check for peak pattern
        else if (a < b && b > c) {

            // b is strictly greater than both a and c
            cout << "PEAK\n";
        }
        // All other cases
        else {

            // Does not satisfy any valid pattern
            cout << "NONE\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| a | b | c | Output | Reasoning               |
| - | - | - | ------ | ----------------------- |
| 1 | 2 | 3 | STAIR  | Strictly increasing     |
| 1 | 3 | 2 | PEAK   | Middle value is highest |
| 2 | 1 | 3 | NONE   | No valid ordering       |
| 5 | 5 | 5 | NONE   | Equal values            |

## Edge Cases to Consider

* All values equal
* Decreasing order
* Duplicate middle value

## Common Test Cases

* `(1, 2, 3)` → STAIR
* `(1, 3, 2)` → PEAK
* `(3, 2, 1)` → NONE

## Common Mistakes to Avoid

* Using non-strict comparisons (`<=` or `>=`)
* Forgetting to handle the default `NONE` case
* Incorrect order of condition checks

## Interview Relevance

* Tests conditional logic accuracy
* Evaluates pattern recognition skills
* Common introductory logic classification problem

## What This Problem Teaches

* Importance of strict inequalities
* Clean branching logic
* Handling multiple exclusive conditions

## Key Takeaways

* Clear conditions lead to reliable solutions
* Always handle fallback cases explicitly
* Order of condition checks matters

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on logical comparisons and condition evaluation, making it suitable for beginners and coding interview warm-ups.