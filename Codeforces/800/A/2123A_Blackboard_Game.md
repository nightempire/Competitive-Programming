## 2123A. Blackboard Game

## Platform

Codeforces

## Problem Link

[Blackboard Game](https://codeforces.com/problemset/problem/2123/A)

## Problem Statement

Alice and Bob are playing a game with a number written on a blackboard.

Given an integer `n`, determine the winner of the game assuming both players play optimally.

The winning condition follows this observation:

* If `n` is divisible by `4`, Bob wins.
* Otherwise, Alice wins.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains a single integer `n`.

## Output Format

* For each test case, print:

  * `"Alice"` if Alice wins
  * `"Bob"` if Bob wins

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 10^9`

## Examples

### Example 1

Input

```id="f6x7uv"
3
1
4
7
```

Explanation

* `1 % 4 ≠ 0` → Alice wins
* `4 % 4 = 0` → Bob wins
* `7 % 4 ≠ 0` → Alice wins

Output

```id="j5t9ms"
Alice
Bob
Alice
```

---

### Example 2

Input

```id="h2w6pl"
2
8
10
```

Explanation

* `8` is divisible by `4` → Bob wins
* `10` is not divisible by `4` → Alice wins

Output

```id="t3v7rx"
Bob
Alice
```

---

### Example 3

Input

```id="n8q0hy"
1
12
```

Explanation

```id="m5u8dg"
12 % 4 = 0
```

So Bob wins.

Output

```id="a4c6ls"
Bob
```

## Approach

Mathematical Observation (Modulo-Based Game Theory)

## Intuition

The game outcome depends entirely on whether `n` is divisible by `4`.

Observation:

* Numbers divisible by `4` are losing states for Alice
* All other numbers are winning states for Alice

Thus:

```text id="r5x3dz"
If n % 4 == 0 → Bob wins
Else → Alice wins
```

No simulation is required.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read integer `n`
  * Check:

    * If `n % 4 == 0` → print `"Bob"`
    * Else → print `"Alice"`

## Visual Walkthrough

### Case 1

```id="l7v8qo"
n = 4
```

```id="v1t9wr"
4 % 4 = 0
Winner = Bob
```

---

### Case 2

```id="u6s3hn"
n = 7
```

```id="p2y5mk"
7 % 4 = 3
Winner = Alice
```

---

### Case 3

```id="x9d1af"
n = 12
```

```id="e4k7qc"
12 % 4 = 0
Winner = Bob
```

## Complexity Analysis

### Time Complexity

**O(1) per test case**

Only one modulo operation is performed.

### Space Complexity

**O(1)**

No additional space is used.

## Solution Explanation

The solution directly applies the mathematical observation derived from the game pattern. By checking divisibility by `4`, the winner can be determined instantly without recursion, dynamic programming, or simulation.

## Full Solution

### C++ Implementation

```cpp id="k8y3rm"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input number
        int n;
        cin >> n;

        // If divisible by 4 → Bob wins
        if(n % 4 == 0) {
            cout << "Bob\n";
        }
        // Otherwise Alice wins
        else {
            cout << "Alice\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| n  | n % 4 | Winner |
| -- | ----- | ------ |
| 1  | 1     | Alice  |
| 4  | 0     | Bob    |
| 7  | 3     | Alice  |
| 8  | 0     | Bob    |
| 12 | 0     | Bob    |

## Edge Cases to Consider

* Minimum value of `n`
* Large values of `n`
* Exact multiples of `4`
* Numbers just greater than multiples of `4`

## Common Test Cases

* `n = 4`
* `n = 8`
* `n = 5`
* `n = 1`

## Common Mistakes to Avoid

* Using incorrect modulo condition
* Overcomplicating with simulation
* Confusing winning and losing states

## Interview Relevance

* Demonstrates game theory observations
* Tests modular arithmetic understanding
* Common competitive programming pattern

## What This Problem Teaches

* Simplifying games using mathematical patterns
* Using modulo operations effectively
* Identifying periodic winning states

## Key Takeaways

* Many game problems reduce to modular patterns
* Observations often eliminate simulation
* Divisibility checks can solve entire problems instantly

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The primary challenge is recognizing the repeating modulo-4 pattern that determines the winner. Once identified, implementation is trivial.