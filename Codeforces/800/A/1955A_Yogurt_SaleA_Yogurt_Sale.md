# A_Yogurt_Sale

## Platform

Codeforces

## Problem Link

[A. Yogurt Sale](https://codeforces.com/problemset/problem/1955/A)

## Problem Statement

A shop sells yogurt in two different ways:

* You can buy **one yogurt** for price `a`
* You can buy **two yogurts together** for price `b`

You want to buy exactly `n` yogurts.

Your task is to calculate the **minimum total cost** to purchase `n` yogurts by choosing the optimal combination of single and double purchases.

## Input Format

* The first line contains an integer `t`, the number of test cases
* For each test case:

  * Three integers `n`, `a`, and `b`

    * `n` — number of yogurts
    * `a` — price of one yogurt
    * `b` — price of two yogurts

## Output Format

* For each test case, print a single integer — the minimum cost

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 100`
* `1 ≤ a, b ≤ 100`

## Examples

### Example 1

Input

```
3
1 5 9
2 5 9
3 5 9
```

Explanation

* Case 1: Buy one yogurt → cost = `5`
* Case 2: Buy two yogurts together → cost = `9`
* Case 3:

  * Buy two yogurts for `9`
  * Buy one yogurt for `5`
  * Total = `14`

Output

```
5
9
14
```

---

### Example 2

Input

```
2
4 3 5
5 3 5
```

Explanation

* Buying two yogurts together is cheaper than buying two separately
* Case 1:

  * `4` yogurts → `2` pairs → `2 × 5 = 10`
* Case 2:

  * `5` yogurts → `2` pairs + `1` single → `2 × 5 + 3 = 13`

Output

```
10
13
```

## Approach

**Greedy Cost Comparison**

## Intuition

For every two yogurts:

* Buying them separately costs `2 × a`
* Buying them together costs `b`

If `b` is cheaper than `2 × a`, it is beneficial to buy yogurts in pairs.

Otherwise, it is better to buy all yogurts individually.

The decision is local and optimal for every pair, making a greedy strategy sufficient.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read `n`, `a`, and `b`
  * If `2 × a > b`:

    * Buy as many pairs as possible
    * If `n` is odd, buy one extra yogurt individually
  * Otherwise:

    * Buy all yogurts individually
* Print the minimum cost

## Visual Walkthrough

### Case 1: `n = 3`, `a = 5`, `b = 9`

```
2 yogurts → pair → cost = 9
1 yogurt  → single → cost = 5
Total = 14
```

---

### Case 2: `n = 4`, `a = 3`, `b = 10`

```
2 × single yogurt = 6 < 10
Buy all individually:
4 × 3 = 12
```

---

### Case 3: `n = 5`, `a = 3`, `b = 5`

```
Pairs are cheaper:
2 pairs → 2 × 5 = 10
1 single → 3
Total = 13
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case

Only constant-time arithmetic and comparisons are performed.

### Space Complexity

**O(1)**

No additional memory is used.

## Solution Explanation

The solution compares the cost of buying two yogurts separately with the cost of buying them as a pair.

* If pair purchase is cheaper, it maximizes pair usage
* If not, it defaults to single purchases

This ensures the minimum total cost for any value of `n`.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int n, a, b;
        cin >> n >> a >> b;

        // If buying two yogurts together is cheaper
        if (a * 2 > b) {

            // If n is odd, one yogurt must be bought separately
            if (n & 1)
                cout << (n / 2) * b + a << '\n';
            else
                cout << (n / 2) * b << '\n';

        } else {
            // Buy all yogurts individually
            cout << n * a << '\n';
        }
    }

    return 0;
}
```

## Test Cases Analysis

| n | a | b | Purchase Strategy | Output |
| - | - | - | ----------------- | ------ |
| 1 | 5 | 9 | Single            | 5      |
| 2 | 5 | 9 | Pair              | 9      |
| 3 | 5 | 9 | Pair + Single     | 14     |
| 4 | 3 | 5 | All Pairs         | 10     |
| 5 | 3 | 5 | Pairs + Single    | 13     |

## Edge Cases to Consider

* `n = 1`
* `2 × a == b`
* Large number of test cases
* Odd vs even values of `n`

## Common Test Cases

* Pair cheaper than singles
* Singles cheaper than pairs
* Mixed cases with odd `n`

## Common Mistakes to Avoid

* Forgetting the odd yogurt case
* Incorrect comparison between `2 × a` and `b`
* Integer division errors

## Interview Relevance

* Demonstrates greedy decision-making
* Tests basic arithmetic optimization
* Common cost-minimization pattern

## What This Problem Teaches

* Greedy strategies for pricing problems
* Importance of comparing bundled vs individual costs
* Handling parity (odd/even cases) correctly

## Key Takeaways

* Always compare bundled prices with individual prices
* Greedy choices work when subproblems are independent
* Simple logic can lead to optimal solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on cost comparison and conditional logic, making it a standard warm-up problem for competitive programming and interviews.