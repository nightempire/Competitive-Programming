## 2060A. Fibonacciness

## Platform

Codeforces

## Problem Link

[A. Fibonacciness](https://codeforces.com/problemset/problem/2060/A)

## Problem Statement

You are given four integers:

```text
a1, a2, a4, a5
```

The value `a3` is unknown and can be chosen arbitrarily.

Define the **fibonacciness** of the sequence as the number of true Fibonacci-like relations among:

```text
a1 + a2 = a3
a2 + a3 = a4
a3 + a4 = a5
```

Your task is to choose a value for `a3` that maximizes the fibonacciness and output the maximum possible value.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains four integers:

```text
a1 a2 a4 a5
```

## Output Format

* For each test case, print a single integer — the maximum possible fibonacciness.

## Constraints

* `1 ≤ t ≤ 10^4`
* `-100 ≤ a1, a2, a4, a5 ≤ 100`

## Examples

### Example 1

Input

```text
3
1 1 3 5
1 2 5 8
2 3 8 13
```

Explanation

#### Test Case 1

Possible choice:

```text
a3 = 2
```

Check relations:

```text
1 + 1 = 2  ✓
1 + 2 = 3  ✓
2 + 3 = 5  ✓
```

Fibonacciness:

```text
3
```

Output

```text
3
```

---

### Example 2

Input

```text
1
1 2 4 7
```

Explanation

Choose:

```text
a3 = 3
```

Relations:

```text
1 + 2 = 3  ✓
2 + 3 = 4  ✗
3 + 4 = 7  ✓
```

Fibonacciness:

```text
2
```

Output

```text
2
```

---

### Example 3

Input

```text
1
5 1 10 20
```

Explanation

No single value of `a3` satisfies all equations.

Best achievable fibonacciness:

```text
1
```

Output

```text
1
```

## Approach

Brute Force on Candidate Values (Mathematical Observation)

## Intuition

There are only three Fibonacci-like conditions:

```text
a1 + a2 = a3
a2 + a3 = a4
a3 + a4 = a5
```

For each condition, we can derive the value of `a3` that would make it true:

From condition 1:

```text
a3 = a1 + a2
```

From condition 2:

```text
a3 = a4 - a2
```

From condition 3:

```text
a3 = a5 - a4
```

These are the only meaningful candidates.

We test each candidate and count how many relations become true.

The maximum count is the answer.

## Algorithm Steps

* Read `t`.
* For each test case:

  * Read `a1`, `a2`, `a4`, `a5`.

  * Generate candidate values:

    ```text
    a1 + a2
    a4 - a2
    a5 - a4
    ```

  * For each candidate:

    * Assume it is `a3`.
    * Count how many of the three Fibonacci relations hold.
    * Update the maximum answer.

  * Print the maximum count.

## Visual Walkthrough

### Case 1

```text
a1=1, a2=1, a4=3, a5=5
```

Candidates:

```text
a1+a2 = 2
a4-a2 = 2
a5-a4 = 2
```

Try:

```text
a3 = 2
```

Check:

```text
1+1=2 ✓
1+2=3 ✓
2+3=5 ✓
```

Fibonacciness:

```text
3
```

---

### Case 2

```text
a1=1, a2=2, a4=4, a5=7
```

Candidates:

```text
3, 2, 3
```

Try:

```text
a3 = 3
```

Check:

```text
1+2=3 ✓
2+3=4 ✗
3+4=7 ✓
```

Fibonacciness:

```text
2
```

---

### Case 3

```text
a1=5, a2=1, a4=10, a5=20
```

Candidates:

```text
6, 9, 10
```

Best candidate satisfies only one equation.

Answer:

```text
1
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case

Only 3 candidate values are tested, and each candidate checks exactly 3 equations.

```text
3 × 3 = 9 operations
```

### Space Complexity

**O(1)**

Only a few integer variables are used.

## Solution Explanation

Each Fibonacci relation uniquely determines a value of `a3`.

Since there are only three relations, there are only three candidate values worth checking:

```text
a1 + a2
a4 - a2
a5 - a4
```

For every candidate:

* Assume it is the missing value.
* Count how many relations become valid.
* Keep the maximum count.

Because the number of candidates is constant, the solution runs in constant time.

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

        // Known elements of the sequence
        int a1, a2, a4, a5;
        cin >> a1 >> a2 >> a4 >> a5;

        // Possible values of a3 derived from
        // each Fibonacci-like condition
        int cand[3] = {
            a1 + a2,
            a4 - a2,
            a5 - a4
        };

        // Maximum fibonacciness
        int ans = 0;

        // Try each candidate
        for(int a3 : cand) {

            int cur = 0;

            // Check first relation
            if(a1 + a2 == a3)
                cur++;

            // Check second relation
            if(a2 + a3 == a4)
                cur++;

            // Check third relation
            if(a3 + a4 == a5)
                cur++;

            // Update answer
            ans = max(ans, cur);
        }

        // Print maximum possible fibonacciness
        cout << ans << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| a1 | a2 | a4 | a5 | Best a3 | Fibonacciness |
| -- | -- | -- | -- | ------- | ------------- |
| 1  | 1  | 3  | 5  | 2       | 3             |
| 1  | 2  | 4  | 7  | 3       | 2             |
| 2  | 3  | 8  | 13 | 5       | 3             |
| 5  | 1  | 10 | 20 | 9       | 1             |
| 0  | 0  | 0  | 0  | 0       | 3             |

## Edge Cases to Consider

* All values are zero.
* Negative numbers.
* Multiple candidates produce the same maximum score.
* All three candidates are identical.
* No candidate satisfies more than one relation.

## Common Test Cases

* Perfect Fibonacci-like sequence.
* Exactly two relations can be satisfied.
* Only one relation can be satisfied.
* Inputs containing negative values.
* Repeated values.

## Common Mistakes to Avoid

* Trying random values of `a3` instead of using derived candidates.
* Forgetting to check all three candidate values.
* Updating the answer without taking the maximum.

## Interview Relevance

* Demonstrates equation manipulation.
* Tests observation-based optimization.
* Reinforces brute force over a small candidate space.

## What This Problem Teaches

* Deriving candidate solutions from constraints.
* Reducing infinite possibilities to a finite set.
* Using mathematical observations to simplify problems.

## Key Takeaways

* Each equation independently suggests a value of `a3`.
* Only three candidate values need to be checked.
* Small brute-force approaches are often optimal when the candidate space is constant.

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The main challenge is recognizing that every Fibonacci-like relation directly determines a candidate value for `a3`. Once these candidates are identified, checking them requires only constant time.