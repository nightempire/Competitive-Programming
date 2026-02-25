# A_Goals_of_Victory

## Platform

Codeforces

## Problem Link

[A. Goals of Victory](https://codeforces.com/problemset/problem/1877/A)

---

## Problem Statement

In a football tournament, there are `n` teams.

It is known that:

* Each team plays against every other team exactly once.
* For every match:

  * One team scores **+1**
  * The other team scores **-1**
* No draws occur.

You are given the final score differences of `n - 1` teams.

Your task is to determine the score difference of the remaining team.

---

## Input Format

* The first line contains an integer `t` — number of test cases.
* For each test case:

  * An integer `n` — number of teams.
  * `n - 1` integers — score differences of the first `n - 1` teams.

---

## Output Format

For each test case, print a single integer — the score difference of the last team.

---

## Constraints

* `1 ≤ t ≤ 10^4`
* `2 ≤ n ≤ 100`
* Score differences are integers in reasonable bounds.

---

## Examples

### Example 1

Input

```
2
3
1 -1
4
1 1 -2
```

Explanation

Test Case 1
Sum of given scores = 1 + (-1) = 0
Since total sum of all teams must be 0,
Missing score = -0 = 0

Test Case 2
Sum of given scores = 1 + 1 + (-2) = 0
Missing score = 0

Output

```
0
0
```

---

### Example 2

Input

```
1
5
2 -1 -1 0
```

Explanation

Sum of given = 2 - 1 - 1 + 0 = 0
Missing score = 0

Output

```
0
```

---

## Approach (Algorithm Type)

**Mathematical Invariant (Sum Property Observation)**

---

## Intuition

In every match:

* One team gets `+1`
* The other team gets `-1`

So the total contribution of each match is:

```
+1 + (-1) = 0
```

Since every match contributes zero to the overall sum,
the sum of score differences of **all teams combined must be 0**.

Therefore:

```
Sum of all n teams = 0
```

If we know the sum of `n - 1` teams:

```
missing_value = - (sum of known values)
```

---

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read integer `n`.
  * Initialize `total = 0`.
  * Read `n - 1` integers.
  * Add each to `total`.
  * Print `-total`.

---

## Visual Walkthrough

### Test Case 1

Input:

```
n = 3
1 -1
```

Compute:

| Team | Score |
| ---- | ----- |
| 1    | 1     |
| 2    | -1    |
| 3    | ?     |

Sum so far:

```
1 + (-1) = 0
```

Since total must be 0:

```
Missing = -0 = 0
```

---

### Test Case 2

Input:

```
n = 4
1 1 -2
```

Compute:

```
1 + 1 - 2 = 0
```

Missing:

```
0
```

---

### Test Case 3

Input:

```
n = 5
3 -2 1 -1
```

Sum:

```
3 - 2 + 1 - 1 = 1
```

Missing:

```
-1
```

---

## Complexity Analysis

### Time Complexity

For each test case:

* Reading `n - 1` integers → O(n)

Overall:

```
O(total n across all test cases)
```

Efficient under constraints.

---

### Space Complexity

```
O(1)
```

Only a single accumulator variable is used.

---

## Solution Explanation

The core observation is a tournament invariant:

* Every match produces a net sum of zero.
* Therefore, total sum across all teams must be zero.

By summing known values and negating the result, we directly obtain the missing score.

No simulation of matches is needed.

---

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

        int n;
        cin >> n;

        // Variable to store sum of known scores
        int total = 0;

        // Read n - 1 score differences
        for(int i = 0; i < n - 1; i++) {

            int num;
            cin >> num;

            total += num;
        }

        // Since total sum must be zero,
        // missing score is negative of current sum
        cout << -total << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| Given Scores | Sum | Missing Score |
| ------------ | --- | ------------- |
| 1 -1         | 0   | 0             |
| 1 1 -2       | 0   | 0             |
| 3 -2 1 -1    | 1   | -1            |
| 5 -3 -1      | 1   | -1            |

---

## Edge Cases to Consider

* Minimum teams (`n = 2`)
* All given scores are zero
* Large positive and negative values
* Sum already zero

---

## Common Test Cases

* Balanced scores
* One large positive value
* One large negative value
* Mixed positive and negative

---

## Common Mistakes to Avoid

* Forgetting that total sum must be zero
* Reading incorrect number of integers
* Not resetting total per test case

---

## Interview Relevance

* Tests ability to detect invariants
* Demonstrates algebraic simplification
* Encourages reasoning instead of simulation

---

## What This Problem Teaches

* Understanding sum invariants
* Leveraging mathematical properties
* Writing minimal and efficient solutions

---

## Key Takeaways

* Many problems reduce to identifying a conserved quantity.
* Always check if a global invariant exists.
* Mathematical reasoning can eliminate brute force.

---

## Problem Difficulty Analysis

This is an **Easy-level** Codeforces problem.

It primarily tests logical reasoning and recognition of a simple mathematical invariant, making it suitable for beginners and quick contest warm-ups.