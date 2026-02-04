# A_Collecting_Coins

## Platform

Codeforces

## Problem Link

[A. Collecting Coins](https://codeforces.com/problemset/problem/1294/A)

## Problem Statement

You are given multiple test cases.
In each test case, four integers `a`, `b`, `c`, and `n` are provided.

* `a`, `b`, and `c` represent the number of coins that three people currently have.
* `n` represents the number of additional coins available to distribute.

Your task is to determine whether it is possible to distribute **all `n` coins** such that **after distribution, all three people have the same number of coins**.

For each test case, print `"YES"` if it is possible, otherwise print `"NO"`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * A single line contains four integers `a`, `b`, `c`, and `n`.

## Output Format

For each test case, output:

* `"YES"` if equal distribution is possible
* `"NO"` otherwise

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 10^4`
* `0 ≤ a, b, c ≤ 10^9`
* `0 ≤ n ≤ 10^9`

## Examples

### Example 1

Input

```
3
1 2 3 3
2 2 2 1
4 4 4 0
```

Explanation

* Test case 1:

  * Maximum coins = `3`
  * Coins needed to equalize = `(3−1)+(3−2)+(3−3)=3`
  * Remaining coins = `3−3=0` → divisible by 3
  * Output → `YES`
* Test case 2:

  * Already equal, but `1` extra coin cannot be evenly distributed
  * Output → `NO`
* Test case 3:

  * Already equal and no extra coins
  * Output → `YES`

Output

```
YES
NO
YES
```

### Example 2

Input

```
2
0 0 0 2
1 5 7 6
```

Explanation

* Test case 1:

  * Extra coins `2` not divisible by 3 → `NO`
* Test case 2:

  * Coins needed to equalize = `(7−1)+(7−5)+(7−7)=8`
  * `8 > 6` → not enough coins → `NO`

Output

```
NO
NO
```

## Approach

**Greedy equalization using maximum value alignment**

## Intuition

To make all three values equal:

* First, bring the smaller values up to the current maximum
* This requires a fixed number of coins
* Any remaining coins must be distributable evenly among all three people

Thus, two conditions must hold:

* Available coins are sufficient to equalize
* Remaining coins are divisible by `3`

## Algorithm Steps

* Read integer `t`
* For each test case:

  * Read `a`, `b`, `c`, and `n`
  * Compute `maxi = max(a, b, c)`
  * Compute coins needed to reach `maxi` for all
  * Check:

    * `need ≤ n`
    * `(n − need) % 3 == 0`
  * Print `"YES"` if both conditions hold, otherwise `"NO"`

## Visual Walkthrough

### Test Case 1

Input:

```
a=1, b=2, c=3, n=3
```

Equalization:

```
Target = 3
Need = (3−1)+(3−2)+(3−3) = 3
Remaining = 3−3 = 0
```

Result:

```
YES
```

---

### Test Case 2

Input:

```
a=2, b=2, c=2, n=1
```

Equalization:

```
Already equal
Remaining = 1 (not divisible by 3)
```

Result:

```
NO
```

---

### Test Case 3

Input:

```
a=1, b=5, c=7, n=6
```

Equalization:

```
Need = (7−1)+(7−5)+(7−7) = 8
8 > 6
```

Result:

```
NO
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case

Only constant-time arithmetic operations are used.

### Space Complexity

**O(1)**

No additional memory proportional to input size is required.

## Solution Explanation

The solution aligns all values to the current maximum because reducing values is not allowed.
After equalization, any leftover coins must be shared equally among three people; otherwise, equality cannot be maintained.

This direct arithmetic check ensures correctness and optimal efficiency.

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

        // Coins held by three people and extra coins
        int a, b, c, n;
        cin >> a >> b >> c >> n;

        // Find the maximum among a, b, and c
        int maxi = max(a, max(b, c));

        // Calculate coins needed to equalize all to maxi
        int need = (maxi - a) + (maxi - b) + (maxi - c);

        // Check if equal distribution is possible
        if (need <= n && (n - need) % 3 == 0) {
            cout << "YES\n";
        } else {
            cout << "NO\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | a b c n | Need | Remaining | Output |
| --------- | ------- | ---- | --------- | ------ |
| 1         | 1 2 3 3 | 3    | 0         | YES    |
| 2         | 2 2 2 1 | 0    | 1         | NO     |
| 3         | 4 4 4 0 | 0    | 0         | YES    |
| 4         | 1 5 7 6 | 8    | —         | NO     |

## Edge Cases to Consider

* All three values already equal
* Not enough coins to reach the maximum
* Remaining coins not divisible by `3`

## Common Test Cases

* Large values of `a`, `b`, `c`
* `n = 0`
* Exactly enough coins to equalize

## Common Mistakes to Avoid

* Forgetting to check divisibility by `3`
* Attempting to reduce values instead of only increasing
* Ignoring the case where coins are insufficient

## Interview Relevance

* Tests greedy reasoning
* Evaluates arithmetic and modular logic
* Common example of feasibility checking

## What This Problem Teaches

* Equalization strategies
* Importance of invariants
* Using math to replace simulation

## Key Takeaways

* Always align values to the maximum when only increments are allowed
* Leftover resources must be distributable evenly
* Simple conditions can fully solve feasibility problems

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on logical reasoning and clean arithmetic rather than complex algorithms.