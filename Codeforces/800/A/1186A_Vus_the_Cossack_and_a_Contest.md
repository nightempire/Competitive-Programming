## Platform

Codeforces

## Problem Link

[A. Vus the Cossack and a Contest](https://codeforces.com/problemset/problem/1186/A)

---

## Problem Statement

Vus the Cossack wants to participate in a contest.

To participate, he needs:

* At least `n` participants
* At least `n` pens
* At least `n` notebooks

You are given three integers:

* `n` → required number of participants
* `m` → number of pens available
* `k` → number of notebooks available

Determine whether Vus can organize the contest.

---

## Input Format

* A single line containing three integers `n`, `m`, and `k`

---

## Output Format

* Print `"Yes"` if the contest can be organized
* Otherwise print `"No"`

---

## Constraints

* `1 ≤ n, m, k ≤ 1000`

---

## Examples

### Example 1

Input

```id="m8x2qp"
3 3 3
```

Explanation

* Participants needed = 3
* Pens available = 3
* Notebooks available = 3

All conditions satisfied

Output

```id="k3z9vt"
Yes
```

---

### Example 2

Input

```id="p6n4mz"
5 3 6
```

Explanation

* Pens are insufficient (`3 < 5`)

Output

```id="t2k8xr"
No
```

---

### Example 3

Input

```id="z7m1qp"
4 5 2
```

Explanation

* Notebooks are insufficient (`2 < 4`)

Output

```id="x5k9vl"
No
```

---

## Approach

Simple condition checking

---

## Intuition

To conduct the contest:

```text id="y3k8vp"
m ≥ n AND k ≥ n
```

If both resources are sufficient, the contest is possible.

---

## Algorithm Steps

* Read `n`, `m`, `k`
* Check:

  * If `n ≤ m` AND `n ≤ k`:

    * Print `"Yes"`
  * Else:

    * Print `"No"`

---

## Visual Walkthrough

### Case 1: `n = 3, m = 3, k = 3`

```text id="r2k9mz"
Pens ≥ n ✔
Notebooks ≥ n ✔

Result → Yes
```

---

### Case 2: `n = 5, m = 3, k = 6`

```text id="p4m8xz"
Pens < n ✘

Result → No
```

---

### Case 3: `n = 4, m = 5, k = 2`

```text id="t6k3zp"
Notebooks < n ✘

Result → No
```

---

## Complexity Analysis

### Time Complexity

O(1)

* Constant-time comparison

---

### Space Complexity

O(1)

* No extra space used

---

## Solution Explanation

The solution directly verifies whether both required resources meet the minimum requirement.

If both conditions hold, the answer is `"Yes"`, otherwise `"No"`.

---

## Full Solution

### C++ Implementation

```cpp id="v9k2zp"
#include<iostream>
using namespace std;

int main() {

    // Input values
    int n, m, k;
    cin >> n >> m >> k;

    // Check if resources are sufficient
    if(n <= m && n <= k) {
        cout << "Yes\n";
    } else {
        cout << "No\n";
    }

    return 0;
}
```

---

## Test Cases Analysis

| n | m | k | Result |
| - | - | - | ------ |
| 3 | 3 | 3 | Yes    |
| 5 | 3 | 6 | No     |
| 4 | 5 | 2 | No     |
| 2 | 5 | 5 | Yes    |

---

## Edge Cases to Consider

* `n = 1`
* `m = n`, `k = n`
* One resource insufficient
* Both resources insufficient

---

## Common Test Cases

* Minimum values
* Exact matches
* One-sided insufficiency

---

## Common Mistakes to Avoid

* Using OR instead of AND
* Misinterpreting conditions
* Incorrect comparison operators

---

## Interview Relevance

* Basic condition checking
* Understanding constraints
* Clean implementation

---

## What This Problem Teaches

* Translating requirements into conditions
* Writing simple and clear logic
* Avoiding overcomplication

---

## Key Takeaways

* Both conditions must be satisfied
* Use logical AND correctly
* Keep logic simple

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Basic comparisons
* Logical operators
* Input/output handling