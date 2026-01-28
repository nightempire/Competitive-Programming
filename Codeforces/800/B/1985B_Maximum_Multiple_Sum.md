# B. Maximum Multiple Sum

## Platform

Codeforces

## Problem Link

[B. Maximum Multiple Sum](https://codeforces.com/problemset/problem/1985/B)

## Problem Statement

You are given multiple test cases.
For each test case, you are given an integer `n`.

For every integer `x` such that `2 ≤ x ≤ n`, consider all positive multiples of `x` that are **less than or equal to `n`**.
Let the sum of these multiples be denoted as `S(x)`.

Your task is to find the value of `x` for which `S(x)` is **maximum**.
If there are multiple such values, output any one of them.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains a single integer `n`.

## Output Format

For each test case, print a single integer — the value of `x` that maximizes the sum of its multiples up to `n`.

## Constraints

* `1 ≤ t ≤ 10^4`
* `2 ≤ n ≤ 10^5`

## Examples

### Example 1

Input

```
3
3
5
10
```

Explanation

* `n = 3`

  * `x = 2`: multiples → `2`, sum = 2
  * `x = 3`: multiples → `3`, sum = 3 → maximum
* `n = 5`

  * `x = 2`: multiples → `2, 4`, sum = 6 → maximum
* `n = 10`

  * `x = 2`: multiples → `2, 4, 6, 8, 10`, sum = 30 → maximum

Output

```
3
2
2
```

### Example 2

Input

```
1
7
```

Explanation

* `x = 2`: multiples → `2, 4, 6`, sum = 12 → maximum

Output

```
2
```

## Approach

Brute-force evaluation using arithmetic series formula.

## Intuition

For a given `x`, all its multiples up to `n` form an arithmetic sequence:

```
x, 2x, 3x, ..., kx
```

where:

```
k = n / x
```

The sum of this sequence can be computed efficiently using the arithmetic series formula.
By evaluating this sum for every valid `x`, the value that produces the maximum sum can be identified.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read integer `n`
  * Initialize variables to track the maximum sum and corresponding `x`
  * For every `x` from `2` to `n`:

    * Compute `k = n / x`
    * Compute sum using the formula
      `sum = x × k × (k + 1) / 2`
    * If this sum is greater than the current maximum, update the answer
  * Output the value of `x` that gives the maximum sum

## Visual Walkthrough

### Test Case 1

Input:

```
n = 6
```

Evaluation:

```
x = 2 → multiples: 2, 4, 6 → sum = 12
x = 3 → multiples: 3, 6 → sum = 9
x = 4 → multiples: 4 → sum = 4
x = 5 → multiples: 5 → sum = 5
x = 6 → multiples: 6 → sum = 6
```

Maximum sum:

```
12 (x = 2)
```

---

### Test Case 2

Input:

```
n = 4
```

Evaluation:

```
x = 2 → multiples: 2, 4 → sum = 6
x = 3 → multiples: 3 → sum = 3
x = 4 → multiples: 4 → sum = 4
```

Result:

```
x = 2
```

## Complexity Analysis

### Time Complexity

O(n) per test case

Each value of `x` from `2` to `n` is evaluated once using constant-time arithmetic.

### Space Complexity

O(1)

Only a few integer variables are used.

## Solution Explanation

The solution systematically checks every possible `x` and computes the sum of its multiples using a mathematical formula rather than iteration.

By tracking the maximum sum and corresponding value of `x`, the algorithm ensures correctness while maintaining efficiency.

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

        // Upper limit
        int n;
        cin >> n;

        // Variables to store maximum sum and corresponding x
        int maxSum = 0;
        int ans = 0;

        // Try all possible x values
        for (int x = 2; x <= n; x++) {

            // Number of multiples of x not exceeding n
            int k = n / x;

            // Sum of multiples using arithmetic series formula
            int sum = x * k * (k + 1) / 2;

            // Update answer if a larger sum is found
            if (sum > maxSum) {
                maxSum = sum;
                ans = x;
            }
        }

        // Output the result
        cout << ans << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n  | Output | Reason                      |
| -- | ------ | --------------------------- |
| 2  | 2      | Only valid x                |
| 3  | 3      | Larger single multiple      |
| 5  | 2      | Best sum with two multiples |
| 7  | 2      | More multiples increase sum |
| 10 | 2      | Maximum cumulative sum      |

## Edge Cases to Consider

* Smallest valid `n = 2`
* Large values of `n`
* Multiple `x` yielding close sums

## Common Test Cases

* Prime values of `n`
* Composite values of `n`
* Large `n` with many divisors

## Common Mistakes to Avoid

* Iterating over multiples instead of using formula
* Forgetting to reset variables per test case
* Integer overflow in sum calculation

## Interview Relevance

* Tests mathematical optimization
* Evaluates use of arithmetic series
* Demonstrates efficient brute-force reasoning

## What This Problem Teaches

* Applying math formulas to optimize loops
* Understanding cumulative effects of multiples
* Translating problem constraints into efficient code

## Key Takeaways

* Arithmetic series formulas save time
* Brute-force can be efficient with math
* Always analyze patterns in sums

## Problem Difficulty Analysis

This is an **Easy-to-Medium (B)** level problem.
It combines basic math with careful iteration and efficient computation.