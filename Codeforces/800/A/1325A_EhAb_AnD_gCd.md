# A_EhAb_AnD_gCd

## Platform

Codeforces

## Problem Link

[A. EhAb AnD gCd](https://codeforces.com/problemset/problem/1325/A)

## Problem Statement

You are given an integer `x`.

Your task is to find two **positive integers** `a` and `b` such that:

```text
a + b = x
```

and

```text
gcd(a, b) + lcm(a, b) = x
```

Where:

* `gcd(a, b)` is the **greatest common divisor**
* `lcm(a, b)` is the **least common multiple**

For each test case, output **any valid pair** `(a, b)` that satisfies the conditions.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each of the next `t` lines contains a single integer:

```text
x
```

## Output Format

For each test case, print two integers:

```text
a b
```

Such that the conditions are satisfied.

## Constraints

* `1 ≤ t ≤ 10^4`
* `2 ≤ x ≤ 10^9`

## Examples

### Example 1

Input

```
3
2
5
10
```

Explanation

Case 1

```
x = 2
```

Choose:

```
a = 1
b = 1
```

Check:

```
a + b = 2
gcd(1,1) = 1
lcm(1,1) = 1
1 + 1 = 2
```

Output

```
1 1
```

---

Case 2

```
x = 5
```

Choose:

```
a = 1
b = 4
```

Check:

```
a + b = 5
gcd(1,4) = 1
lcm(1,4) = 4
1 + 4 = 5
```

Output

```
1 4
```

---

Case 3

```
x = 10
```

Choose:

```
a = 1
b = 9
```

Check:

```
a + b = 10
gcd(1,9) = 1
lcm(1,9) = 9
1 + 9 = 10
```

Output

```
1 9
```

## Approach

Mathematical Construction using GCD–LCM Properties

## Intuition

We want:

```
a + b = x
```

and

```
gcd(a, b) + lcm(a, b) = x
```

If we choose:

```
a = 1
b = x - 1
```

Then:

```
gcd(1, x-1) = 1
```

because `1` divides every integer.

And:

```
lcm(1, x-1) = x - 1
```

Thus:

```
gcd + lcm
= 1 + (x - 1)
= x
```

So the condition is always satisfied.

Therefore the pair:

```
(1, x-1)
```

is a valid answer for every `x ≥ 2`.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read integer `x`.
  * Print:

```
1 x-1
```

## Visual Walkthrough

### Test Case 1

Input

```
x = 6
```

Choose:

```
a = 1
b = 5
```

Check

```
a + b = 6
gcd(1,5) = 1
lcm(1,5) = 5
```

Sum

```
1 + 5 = 6
```

Valid pair.

---

### Test Case 2

Input

```
x = 8
```

Choose:

```
a = 1
b = 7
```

Check

```
gcd(1,7) = 1
lcm(1,7) = 7
```

Result

```
1 + 7 = 8
```

---

### Test Case 3

Input

```
x = 12
```

Choose:

```
a = 1
b = 11
```

Check

```
gcd(1,11) = 1
lcm(1,11) = 11
```

Result

```
1 + 11 = 12
```

## Complexity Analysis

### Time Complexity

```
O(t)
```

Each test case requires only constant-time operations.

### Space Complexity

```
O(1)
```

Only a few variables are used.

## Solution Explanation

The solution leverages a mathematical property of `1`.

Since:

```
gcd(1, n) = 1
lcm(1, n) = n
```

choosing:

```
a = 1
b = x - 1
```

guarantees that:

```
gcd(a,b) + lcm(a,b) = x
```

This eliminates the need for any complex computation.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t, x;

    cin >> t;

    while(t--) {

        // Read value of x
        cin >> x;

        // Choose a = 1 and b = x - 1
        // This always satisfies the required conditions
        cout << 1 << " " << x - 1 << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| x  | a | b  | gcd(a,b) | lcm(a,b) | gcd + lcm |
| -- | - | -- | -------- | -------- | --------- |
| 2  | 1 | 1  | 1        | 1        | 2         |
| 5  | 1 | 4  | 1        | 4        | 5         |
| 10 | 1 | 9  | 1        | 9        | 10        |
| 12 | 1 | 11 | 1        | 11       | 12        |

## Edge Cases to Consider

* Minimum value `x = 2`
* Large values near `10^9`
* Multiple test cases

## Common Test Cases

* `2`
* `5`
* `10`
* `100`

## Common Mistakes to Avoid

* Trying to compute actual GCD/LCM unnecessarily
* Overcomplicating the solution
* Forgetting that `1` works with every integer

## Interview Relevance

* Demonstrates mathematical insight
* Encourages looking for simple constructions
* Tests understanding of GCD and LCM properties

## What This Problem Teaches

* Recognizing useful number theory identities
* Simplifying problems using mathematical observations
* Avoiding unnecessary computation

## Key Takeaways

* `gcd(1, n) = 1`
* `lcm(1, n) = n`
* Simple constructions can satisfy complex conditions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The main challenge is recognizing the mathematical property that allows the pair `(1, x-1)` to always satisfy the required conditions. Once identified, the implementation becomes trivial.