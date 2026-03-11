# A_Add_Odd_or_Subtract_Even

## Platform

Codeforces

## Problem Link

[A. Add Odd or Subtract Even](https://codeforces.com/problemset/problem/1311/A)

## Problem Statement

You are given two integers `a` and `b`.

In one operation, you can perform one of the following:

* Add any **odd integer** to `a`.
* Subtract any **even integer** from `a`.

Your goal is to transform `a` into `b` using the **minimum number of operations**.

For each test case, determine the **minimum number of operations required**.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each test case consists of one line containing two integers:

```id="m2ay5y"
a b
```

## Output Format

For each test case, print a single integer — the **minimum number of operations required**.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ a, b ≤ 10^9`

## Examples

### Example 1

Input

```id="0p5r3a"
3
2 3
5 3
4 4
```

Explanation

Case 1

```id="1xmy89"
a = 2, b = 3
```

Add `1` (odd number):

```id="c1k6j5"
2 + 1 = 3
```

Operations:

```id="edjzkc"
1
```

---

Case 2

```id="sk4n9u"
a = 5, b = 3
```

Subtract `2` (even number):

```id="bbpn9p"
5 - 2 = 3
```

Operations:

```id="y7q7go"
1
```

---

Case 3

```id="4d8ys1"
a = 4, b = 4
```

Already equal.

Operations:

```id="x9j5h0"
0
```

Output

```id="82y3ap"
1
1
0
```

---

### Example 2

Input

```id="s7twc4"
2
10 4
3 10
```

Explanation

Case 1

```id="pgrh22"
a = 10, b = 4
diff = 6 (even)
```

Subtract `6` in one operation.

Result:

```id="o7spgu"
1
```

Case 2

```id="tdq8rd"
a = 3, b = 10
diff = -7
```

Add `7` (odd number):

```id="rcc9k5"
3 + 7 = 10
```

Result:

```id="7mbsx6"
1
```

Output

```id="g9ac6a"
1
1
```

---

### Example 3

Input

```id="u0p9cn"
2
8 3
6 9
```

Explanation

Case 1

```id="9m8njq"
a = 8, b = 3
diff = 5 (odd)
```

Cannot subtract odd numbers.

Steps:

```
8 - 2 = 6
6 - 4 = 2
2 + 1 = 3
```

Minimum operations = **2** (optimal sequence).

Output:

```id="zv2puu"
2
```

Case 2

```id="t4hxre"
a = 6, b = 9
diff = -3 (odd)
```

Add `3`:

```id="l9ucv1"
6 + 3 = 9
```

Operations:

```id="bnzvga"
1
```

Output

```id="qdfqph"
2
1
```

## Approach

Parity-Based Greedy Logic

## Intuition

Let:

```id="mgt2q5"
diff = a - b
```

There are three cases.

### Case 1 — `a == b`

No operation is required.

### Case 2 — `a > b`

We must **decrease `a`**.

We are allowed to subtract **even numbers only**.

* If `diff` is **even**, we can subtract it directly in one operation.
* If `diff` is **odd**, we cannot subtract it directly, so we need two operations.

### Case 3 — `a < b`

We must **increase `a`**.

We can add **odd numbers only**.

* If `(b - a)` is **odd**, we can reach `b` in one operation.
* If `(b - a)` is **even**, we need two operations.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read integers `a` and `b`.
  * If `a == b`:

    * Output `0`.
  * Else if `a > b`:

    * Compute `diff = a - b`.
    * If `diff` is even → print `1`.
    * Else → print `2`.
  * Else (`a < b`):

    * Compute `diff = b - a`.
    * If `diff` is odd → print `1`.
    * Else → print `2`.

## Visual Walkthrough

### Test Case 1

Input

```id="tsxt03"
a = 2, b = 3
```

Difference

```id="cv1kda"
b - a = 1 (odd)
```

Operation

```id="h22s1y"
2 + 1 = 3
```

Operations:

```id="5j9t9p"
1
```

---

### Test Case 2

Input

```id="t1pkf1"
a = 5, b = 3
```

Difference

```id="k7y9n7"
a - b = 2 (even)
```

Operation

```id="1o1q2d"
5 - 2 = 3
```

Operations:

```id="6ho5is"
1
```

---

### Test Case 3

Input

```id="rr5t9a"
a = 8, b = 3
```

Difference

```id="5wd4yu"
5 (odd)
```

Not directly subtractable.

Minimum operations:

```id="ww9ja8"
2
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case is processed in constant time.

### Space Complexity

O(1)

Only a few integer variables are used.

## Solution Explanation

The solution determines the relationship between `a` and `b`.

Instead of simulating operations, it uses **parity properties** of odd and even numbers to determine the minimal number of steps.

By analyzing whether the difference between the numbers is odd or even, the program directly computes the optimal number of operations.

This leads to a highly efficient constant-time solution.

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

        // Read integers a and b
        int a, b;
        cin >> a >> b;

        // Difference between the numbers
        int diff = a - b;

        // Variable to store minimum operations
        int ops = 0;

        // Case when a is greater than b
        if (a > b) {

            // If difference is odd, need two operations
            if (diff & 1)
                ops = 2;

            // If difference is even, one operation is enough
            else
                ops = 1;
        }

        // Case when b is greater than a
        else if (b > a) {

            // If difference is odd, one operation is enough
            if (diff & 1)
                ops = 1;

            // If difference is even, need two operations
            else
                ops = 2;
        }

        // Print result
        cout << ops << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| a | b | Difference | Result |
| - | - | ---------- | ------ |
| 2 | 3 | 1 (odd)    | 1      |
| 5 | 3 | 2 (even)   | 1      |
| 8 | 3 | 5 (odd)    | 2      |
| 6 | 9 | 3 (odd)    | 1      |
| 4 | 4 | 0          | 0      |

## Edge Cases to Consider

* `a == b`
* Large values near `10^9`
* Differences equal to `1`
* Differences with large even values

## Common Test Cases

* `2 3`
* `5 3`
* `4 4`
* `10 4`
* `6 9`

## Common Mistakes to Avoid

* Forgetting the `a == b` case
* Using incorrect parity checks
* Confusing the direction of operations

## Interview Relevance

* Demonstrates reasoning with parity
* Shows how to simplify operations mathematically
* Encourages constant-time problem solving

## What This Problem Teaches

* Recognizing patterns in operations
* Leveraging odd/even properties
* Avoiding unnecessary simulation

## Key Takeaways

* Mathematical observations can drastically simplify problems
* Always analyze operation constraints carefully
* Parity logic is powerful in algorithm design

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The main challenge lies in recognizing the parity-based behavior of the operations, after which the implementation becomes straightforward.