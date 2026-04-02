## Platform

Codeforces

## Problem Link

[A. Three Pairwise Maximums](https://codeforces.com/problemset/problem/1385/A)

---

## Problem Statement

You are given three integers `x`, `y`, and `z`.

These represent the **pairwise maximums** of three unknown integers `a`, `b`, and `c`:

```text
max(a, b) = x  
max(b, c) = y  
max(a, c) = z
```

Your task is to determine whether such integers `a`, `b`, and `c` exist.

* If possible:

  * Print `"YES"`
  * Print any valid values of `a`, `b`, `c`
* Otherwise:

  * Print `"NO"`

---

## Input Format

* The first line contains an integer `t` — number of test cases
* Each test case contains three integers `x`, `y`, `z`

---

## Output Format

For each test case:

* Print `"YES"` and a valid triple `a b c`
* Or print `"NO"`

---

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ x, y, z ≤ 10^9`

---

## Examples

### Example 1

Input

```id="x7c2kp"
3
3 3 3
1 2 3
5 5 3
```

Explanation

* Case 1:

  * All equal → possible → `a = b = c = 3`
* Case 2:

  * Only one maximum value appears once → impossible
* Case 3:

  * Two equal maximums → valid

Output

```id="u9b2m1"
YES
3 3 3
NO
YES
5 3 3
```

---

### Example 2

Input

```id="m2z8vp"
2
4 4 2
7 7 7
```

Explanation

* First case → two maximums equal → valid
* Second case → all equal → valid

Output

```id="r5k1qn"
YES
4 2 2
YES
7 7 7
```

---

### Example 3

Input

```id="z4t8ah"
1
10 5 10
```

Explanation

* Two maximums = 10 → valid

Output

```id="d9v3pw"
YES
10 5 5
```

---

## Approach

Greedy observation based on maximum frequency

---

## Intuition

We are given:

```text
max(a, b), max(b, c), max(a, c)
```

Key observation:

* The **largest value must appear at least twice**
* Otherwise, it's impossible to construct such `a, b, c`

Why?

* Each pairwise max depends on the largest elements
* If the largest appears only once → cannot satisfy all three conditions

---

## Algorithm Steps

* Read `t`

* For each test case:

  * Read `x, y, z`
  * Find:

    * Maximum value `mx`
    * Count how many times `mx` appears

* Case analysis:

  * If `mx` appears only once:

    * Print `"NO"`
  * If `mx` appears twice:

    * Let smallest value be `mn`
    * Print:

      ```
      mx mn mn
      ```
  * If all three equal:

    * Print:

      ```
      mx mx mx
      ```

---

## Visual Walkthrough

### Case 1: `(3, 3, 3)`

```id="0f4jzt"
All equal → a = b = c = 3
```

---

### Case 2: `(1, 2, 3)`

```id="q8d9hz"
Max = 3 appears once → impossible
```

---

### Case 3: `(5, 5, 3)`

```id="c2y8xk"
Max = 5 appears twice

Construct:
a = 5
b = 3
c = 3
```

---

## Complexity Analysis

### Time Complexity

O(1) per test case

* Only constant operations

---

### Space Complexity

O(1)

* No extra space used

---

## Solution Explanation

The solution relies on identifying whether the largest value among `x, y, z` appears at least twice.

* If not → impossible
* If yes → construct valid `a, b, c` using:

  * Largest value as dominant element
  * Smallest value to fill remaining positions

This ensures all pairwise maximum conditions are satisfied.

---

## Full Solution

### C++ Implementation

```cpp id="6k3t9p"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input values
        int x, y, z;
        cin >> x >> y >> z;

        // Find maximum and minimum
        int mx = max(x, max(y, z));
        int mn = min(x, min(y, z));

        // Count occurrences of maximum
        int count = (mx == x) + (mx == y) + (mx == z);

        // If maximum appears only once → impossible
        if(count == 1) {
            cout << "NO\n";
        }

        // If maximum appears twice
        else if(count == 2) {
            cout << "YES\n";
            cout << mx << ' ' << mn << ' ' << mn << '\n';
        }

        // If all are equal
        else {
            cout << "YES\n";
            cout << mx << ' ' << mx << ' ' << mx << '\n';
        }
    }

    return 0;
}
```

---

## Test Cases Analysis

| x y z | Max Count | Output    |
| ----- | --------- | --------- |
| 3 3 3 | 3         | YES 3 3 3 |
| 1 2 3 | 1         | NO        |
| 5 5 3 | 2         | YES 5 3 3 |
| 7 7 7 | 3         | YES 7 7 7 |

---

## Edge Cases to Consider

* All values equal
* Maximum appears only once
* Large input values

---

## Common Test Cases

* `(1,1,1)` → YES
* `(1,2,3)` → NO
* `(2,2,1)` → YES

---

## Common Mistakes to Avoid

* Not counting frequency of maximum correctly
* Using wrong values while constructing result
* Ignoring the case when all values are equal

---

## Interview Relevance

* Logical deduction problems
* Constructive algorithms
* Understanding constraints-based construction

---

## What This Problem Teaches

* Pattern recognition in constraints
* Constructing valid solutions from conditions
* Efficient decision-making logic

---

## Key Takeaways

* Maximum must appear at least twice
* Construction depends on frequency of max
* Simple logic can solve complex-looking problems

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Logical reasoning
* Conditional checks
* Constructive thinking