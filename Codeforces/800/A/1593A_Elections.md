## 1593A. Elections

## Platform

Codeforces

## Problem Link

[A. Elections](https://codeforces.com/problemset/problem/1593/A)

## Problem Statement

Three candidates are participating in an election and currently have:

* `a` votes
* `b` votes
* `c` votes

For each candidate, determine the **minimum number of additional votes** they need so that they become the **strict winner**, i.e., have strictly more votes than every other candidate.

For each test case, output three integers corresponding to candidates `a`, `b`, and `c`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains three integers `a`, `b`, and `c`.

## Output Format

For each test case, print three integers:

```text
x y z
```

Where:

* `x` = minimum votes needed for candidate `a`
* `y` = minimum votes needed for candidate `b`
* `z` = minimum votes needed for candidate `c`

to become the unique winner.

## Constraints

* `1 ≤ t ≤ 10^4`
* `0 ≤ a, b, c ≤ 10^9`

## Examples

### Example 1

Input

```text
3
0 0 0
10 75 15
13 13 17
```

Explanation

#### Test Case 1

Current votes:

```text
a = 0
b = 0
c = 0
```

All candidates are tied.

To become the unique winner, each candidate needs:

```text
0 → 1
```

So:

```text
1 1 1
```

Output

```text
1 1 1
```

---

#### Test Case 2

Current votes:

```text
a = 10
b = 75
c = 15
```

Maximum votes:

```text
75
```

Candidate `b` is already the unique leader.

```text
a needs 66 votes  → 76
b needs 0 votes
c needs 61 votes  → 76
```

Output

```text
66 0 61
```

---

### Example 2

Input

```text
1
5 5 3
```

Explanation

Maximum votes:

```text
5
```

Two candidates share the lead.

```text
a needs 1 vote
b needs 1 vote
c needs 3 votes
```

Output

```text
1 1 3
```

---

### Example 3

Input

```text
1
7 2 7
```

Explanation

Maximum votes:

```text
7
```

Candidates `a` and `c` are tied.

```text
a needs 1 vote
b needs 6 votes
c needs 1 vote
```

Output

```text
1 6 1
```

## Approach

Mathematical Observation (Maximum Value Analysis)

## Intuition

To become the **strict winner**, a candidate must have:

```text
votes > current maximum votes among all candidates
```

Let:

```text
maxi = max(a, b, c)
```

Cases:

* If a candidate is the **only** one having `maxi`, they already win and need `0` votes.
* Otherwise, they must reach:

```text
maxi + 1
```

Therefore:

```text
required = maxi - current_votes + 1
```

## Algorithm Steps

* Read `t`.
* For each test case:

  * Read `a`, `b`, and `c`.
  * Compute:

    ```text
    maxi = max(a, b, c)
    ```
  * Count how many candidates have value `maxi`.
  * For each candidate:

    * If they are the unique maximum:

      ```text
      answer = 0
      ```

    * Otherwise:

      ```text
      answer = maxi - votes + 1
      ```
  * Print the three answers.

## Visual Walkthrough

### Case 1

```text
a = 10
b = 75
c = 15
```

Maximum:

```text
75
```

Unique maximum:

```text
b
```

Required votes:

```text
a = 75 - 10 + 1 = 66
b = 0
c = 75 - 15 + 1 = 61
```

Answer:

```text
66 0 61
```

---

### Case 2

```text
a = 5
b = 5
c = 3
```

Maximum:

```text
5
```

Leaders:

```text
a and b
```

Both need one more vote:

```text
a = 1
b = 1
c = 3
```

Answer:

```text
1 1 3
```

---

### Case 3

```text
a = 0
b = 0
c = 0
```

Maximum:

```text
0
```

All tied.

Each candidate needs:

```text
1
```

Answer:

```text
1 1 1
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case

Only a few comparisons and arithmetic operations are performed.

### Space Complexity

**O(1)**

No additional data structures are used.

## Solution Explanation

The solution first finds the maximum vote count among the three candidates.

If exactly one candidate owns this maximum value, that candidate already has strictly more votes than the others and therefore requires `0` additional votes.

For every other case, a candidate must surpass the current maximum by one vote. Thus the required number of votes is:

```text
maxi - current_votes + 1
```

This directly yields the minimum number of additional votes needed.

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

        // Current votes of the three candidates
        int a, b, c;
        cin >> a >> b >> c;

        // Find the maximum vote count
        int maxi = max(a, max(b, c));

        // Count how many candidates have the maximum votes
        int count =
            (a == maxi) +
            (b == maxi) +
            (c == maxi);

        // Candidate A
        cout << (maxi == a && count == 1
                    ? 0
                    : maxi - a + 1)
             << ' ';

        // Candidate B
        cout << (maxi == b && count == 1
                    ? 0
                    : maxi - b + 1)
             << ' ';

        // Candidate C
        cout << (maxi == c && count == 1
                    ? 0
                    : maxi - c + 1)
             << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| a  | b  | c  | Maximum | Output  |
| -- | -- | -- | ------- | ------- |
| 0  | 0  | 0  | 0       | 1 1 1   |
| 10 | 75 | 15 | 75      | 66 0 61 |
| 13 | 13 | 17 | 17      | 5 5 0   |
| 5  | 5  | 3  | 5       | 1 1 3   |
| 7  | 2  | 7  | 7       | 1 6 1   |

## Edge Cases to Consider

* All three candidates have equal votes.
* Two candidates share the maximum.
* One candidate is already the unique winner.
* One or more candidates have zero votes.
* Very large vote counts.

## Common Test Cases

* `(0, 0, 0)`
* `(5, 5, 5)`
* `(10, 20, 30)`
* `(7, 7, 3)`
* `(100, 1, 100)`

## Common Mistakes to Avoid

* Returning `0` for all maximum-valued candidates when there is a tie.
* Forgetting the `+1` needed to become a **strict** winner.
* Not counting how many candidates share the maximum value.

## Interview Relevance

* Tests handling of maximum values and ties.
* Demonstrates careful implementation of mathematical conditions.
* Reinforces edge-case analysis.

## What This Problem Teaches

* Working with maxima and tie conditions.
* Converting problem statements into direct formulas.
* Handling strict inequality requirements correctly.

## Key Takeaways

* A unique maximum requires no additional votes.
* Tied leaders still need one extra vote to become the sole winner.
* Careful edge-case handling is often more important than complex algorithms.

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The solution is based on a simple mathematical observation. The main challenge is correctly handling tie situations and ensuring that candidates become **strictly** greater than all others.