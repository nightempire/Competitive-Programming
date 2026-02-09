# A_Grasshopper_on_a_Line

## Platform

Codeforces

## Problem Link

[A. Grasshopper on a Line](https://codeforces.com/problemset/problem/1837/A)

## Problem Statement

A grasshopper starts at position `0` on a number line.

You are given two integers `x` and `k`.
You must represent the number `x` as a sum of **one or more positive integers** such that **none of the chosen integers is divisible by `k`**.

Your task is to output:

* The number of integers used
* The integers themselves

It is guaranteed that a solution always exists.

## Input Format

* The first line contains an integer `t`, the number of test cases
* For each test case:

  * Two integers `x` and `k`

## Output Format

For each test case:

* Print an integer `m` — the number of integers used
* Print `m` positive integers whose sum is `x`
* None of the printed integers should be divisible by `k`

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ x ≤ 10^9`
* `2 ≤ k ≤ 10^9`

## Examples

### Example 1

Input

```
2
5 3
6 3
```

Explanation

**Test case 1:**
`x = 5`, `k = 3`
Since `5 % 3 ≠ 0`, we can directly use `5`.

**Test case 2:**
`x = 6`, `k = 3`
Since `6 % 3 = 0`, `6` cannot be used directly.
Split it as `5 + 1`.

Output

```
1
5
2
5 1
```

## Approach

**Greedy Construction Based on Divisibility Check**

## Intuition

There are only two possible situations:

* If `x` is **not divisible by `k`**:

  * We can represent `x` using a single number — `x` itself
* If `x` **is divisible by `k`**:

  * Using `x` directly is invalid
  * Splitting `x` into `(x - 1)` and `1` always works because:

    * `1` is never divisible by `k`
    * `(x - 1) % k ≠ 0` when `x % k = 0`

Thus, the answer always uses either **1 or 2 numbers**.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read `x` and `k`
  * If `x % k ≠ 0`:

    * Output `1`
    * Output `x`
  * Else:

    * Output `2`
    * Output `(x - 1)` and `1`

## Visual Walkthrough

### Case 1: `x = 7`, `k = 4`

```
7 % 4 ≠ 0
Answer: [7]
```

---

### Case 2: `x = 8`, `k = 4`

```
8 % 4 = 0
Split into: 7 + 1
Both are not divisible by 4
```

---

### Case 3: `x = 2`, `k = 2`

```
2 % 2 = 0
Split into: 1 + 1
Valid
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case

Only constant-time arithmetic and condition checks are performed.

### Space Complexity

**O(1)**

No extra data structures are used.

## Solution Explanation

The solution relies on a simple divisibility observation.

Instead of searching for multiple combinations, it directly:

* Uses `x` if valid
* Otherwise splits `x` into two guaranteed valid numbers

This ensures correctness, simplicity, and optimal performance.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int x, k;
        cin >> x >> k;

        // If x is not divisible by k, use x directly
        if (x % k != 0) {
            cout << "1\n";
            cout << x << '\n';
        } 
        // Otherwise, split x into (x - 1) and 1
        else {
            cout << "2\n";
            cout << x - 1 << " 1\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| x | k | Output Count | Representation |
| - | - | ------------ | -------------- |
| 5 | 3 | 1            | 5              |
| 6 | 3 | 2            | 5 1            |
| 7 | 4 | 1            | 7              |
| 8 | 4 | 2            | 7 1            |

## Edge Cases to Consider

* `x = 1`
* `x = k`
* Very large values of `x`
* Multiple test cases

## Common Test Cases

* `x` divisible by `k`
* `x` not divisible by `k`
* Smallest possible values

## Common Mistakes to Avoid

* Forgetting that `1` is never divisible by `k`
* Overcomplicating the solution
* Printing unnecessary extra numbers

## Interview Relevance

* Tests mathematical reasoning
* Evaluates divisibility logic
* Demonstrates greedy problem solving

## What This Problem Teaches

* Using simple observations to avoid brute force
* Handling divisibility constraints cleanly
* Writing concise and correct logic

## Key Takeaways

* Many problems reduce to simple case analysis
* Greedy solutions can be optimal with correct reasoning
* Always look for minimal constructions first

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The challenge lies in recognizing the guaranteed valid split and applying it correctly with minimal logic.