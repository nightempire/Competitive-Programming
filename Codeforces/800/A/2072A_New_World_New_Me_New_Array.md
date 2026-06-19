# A. New World, New Me, New Array

## Platform

Codeforces

## Problem Link

[A. New World, New Me, New Array - Codeforces Problem 2072A](https://codeforces.com/problemset/problem/2072/A?utm_source=chatgpt.com)

## Problem Statement

You are given three integers:

* `a` — the maximum number of operations that can be performed.
* `k` — the target value that needs to be reached.
* `p` — the maximum absolute value that can be added or subtracted in a single operation.

In one operation, you may choose any integer `x` such that:

```text
-p ≤ x ≤ p
```

and add it to the current value.

Initially, the value is `0`.

Determine the minimum number of operations required to obtain the value `k`.

If it is impossible to obtain `k` within at most `a` operations, print `-1`.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each test case contains three integers:

```text
a k p
```

## Output Format

For each test case, print:

* The minimum number of operations required to reach `k`, or
* `-1` if it is impossible.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ a ≤ 100`
* `-1000 ≤ k ≤ 1000`
* `1 ≤ p ≤ 100`

## Examples

### Example 1

Input

```text
3
5 12 3
4 10 3
2 -7 4
```

Output

```text
4
-1
2
```

### Explanation

#### Test Case 1

```text
a = 5
k = 12
p = 3
```

Maximum contribution per operation:

```text
3
```

Minimum operations needed:

```text
ceil(12 / 3) = 4
```

Possible sequence:

```text
+3 +3 +3 +3 = 12
```

Output:

```text
4
```

---

#### Test Case 2

```text
a = 4
k = 10
p = 3
```

Maximum achievable magnitude:

```text
4 × 3 = 12
```

Actually possible in 4 operations? Need:

```text
ceil(10 / 3) = 4
```

Output:

```text
4
```

---

#### Test Case 3

```text
a = 2
k = -7
p = 4
```

Using absolute value:

```text
|k| = 7
```

Minimum operations:

```text
ceil(7 / 4) = 2
```

Possible sequence:

```text
-4 -3 = -7
```

Output:

```text
2
```

## Approach

### Algorithm Type

Greedy Mathematics (Ceiling Division)

## Intuition

Since a single operation can contribute at most `p` toward the target, the fastest way to reach `k` is to use the largest possible magnitude in each operation.

Only the absolute value of `k` matters because positive and negative movements are symmetric.

To determine feasibility:

* Maximum reachable magnitude using `a` operations is:

```text
a × p
```

* If:

```text
a × p < |k|
```

then reaching `k` is impossible.

Otherwise, the minimum number of operations required is:

```text
ceil(|k| / p)
```

which can be computed efficiently using integer arithmetic.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read `a`, `k`, and `p`.
  * Convert `k` to `|k|`.
  * Compute maximum reachable magnitude:

```text
a × p
```

* If `a × p < |k|`:

  * Print `-1`.
* Otherwise:

  * Print:

```text
(|k| + p - 1) / p
```

```
which represents ceiling division.
```

## Visual Walkthrough

### Test Case 1

Input:

```text
a = 5
k = 12
p = 3
```

Maximum reachable magnitude:

```text
5 × 3 = 15
```

Since:

```text
15 ≥ 12
```

Target is reachable.

Operations needed:

```text
ceil(12 / 3) = 4
```

Result:

```text
4
```

---

### Test Case 2

Input:

```text
a = 2
k = 9
p = 4
```

Maximum reachable magnitude:

```text
2 × 4 = 8
```

Since:

```text
8 < 9
```

Target cannot be reached.

Result:

```text
-1
```

---

### Test Case 3

Input:

```text
a = 3
k = -7
p = 4
```

Convert:

```text
|k| = 7
```

Maximum reachable magnitude:

```text
3 × 4 = 12
```

Reachable.

Operations:

```text
ceil(7 / 4) = 2
```

Possible moves:

```text
-4 -3
```

Result:

```text
2
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case.

The solution performs only:

* Absolute value computation
* Multiplication
* Comparison
* Ceiling division

Thus:

```text
O(1)
```

For all test cases:

```text
O(t)
```

### Space Complexity

**O(1)**

Only a few integer variables are used.

No additional data structures are required.

## Solution Explanation

The solution first converts `k` into its absolute value because moving positively or negatively requires the same number of operations.

The maximum magnitude achievable with `a` operations is:

```text
a × p
```

If this value is smaller than `|k|`, reaching the target is impossible.

Otherwise, the minimum number of operations is obtained by repeatedly using the maximum allowed magnitude `p`.

Mathematically:

```text
ceil(|k| / p)
```

The implementation computes this using:

```text
(|k| + p - 1) / p
```

which is the standard integer ceiling-division formula.

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

        // Read input values
        int a, k, p;
        cin >> a >> k >> p;

        // Only magnitude matters
        k = abs(k);

        // Check if target can be reached
        if(a * p >= k) {

            // Minimum operations using ceiling division
            cout << (k + p - 1) / p << '\n';
        }
        else {

            // Impossible to reach target
            cout << -1 << '\n';
        }
    }

    return 0;
}
```

## Test Cases Analysis

| a  | k  | p | Maximum Reach (`a×p`) | Minimum Operations | Output |
| -- | -- | - | --------------------- | ------------------ | ------ |
| 5  | 12 | 3 | 15                    | 4                  | 4      |
| 2  | 9  | 4 | 8                     | Impossible         | -1     |
| 3  | -7 | 4 | 12                    | 2                  | 2      |
| 1  | 5  | 5 | 5                     | 1                  | 1      |
| 10 | 0  | 3 | 30                    | 0                  | 0      |

## Edge Cases to Consider

* `k = 0`
* `|k| = p`
* `|k| < p`
* `|k| > a × p`
* Negative values of `k`
* Maximum allowed values of `a`, `k`, and `p`

## Common Test Cases

### Target Already Reached

```text
Input:
1
5 0 3

Output:
0
```

---

### Exact Reachability

```text
Input:
1
2 8 4

Output:
2
```

---

### Impossible Case

```text
Input:
1
2 10 4

Output:
-1
```

---

### Negative Target

```text
Input:
1
3 -7 4

Output:
2
```

## Common Mistakes to Avoid

* Forgetting to use the absolute value of `k`.
* Using normal division instead of ceiling division.
* Checking only the minimum operations without verifying feasibility (`a × p ≥ |k|`).

## Interview Relevance

* Demonstrates mathematical optimization.
* Tests understanding of ceiling division.
* Reinforces feasibility-check patterns commonly used in greedy problems.

## What This Problem Teaches

* Converting a problem into a mathematical model.
* Using ceiling division correctly.
* Separating feasibility checks from optimization calculations.

## Key Takeaways

* Maximum achievable magnitude after `a` operations is `a × p`.
* The minimum required operations are obtained using the largest possible move each time.
* Ceiling division is a common technique in competitive programming.

## Problem Difficulty Analysis

This is an **Easy** mathematics-based problem.

The primary observation is that only the magnitude of the target matters. Once the maximum achievable value and the ceiling-division formula are identified, the implementation becomes very short and efficient. The challenge lies in recognizing the mathematical simplification rather than performing any complex computation.