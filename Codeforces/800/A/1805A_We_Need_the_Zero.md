## 1805A. We Need the Zero

## Platform

Codeforces

## Problem Link

[We Need the Zero](https://codeforces.com/problemset/problem/1805/A)

## Problem Statement

You are given an array of integers.

Find an integer `x` such that:

```text
(a1 XOR x) XOR (a2 XOR x) XOR ... XOR (an XOR x) = 0
```

If such an integer exists, print any valid value of `x`. Otherwise, print `-1`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`, the size of the array.
  * The second line contains `n` integers.

## Output Format

* For each test case, print:

  * A valid integer `x`, or
  * `-1` if no such integer exists.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 2 × 10^5`
* `0 ≤ ai ≤ 10^9`
* Sum of all `n` across test cases does not exceed `2 × 10^5`

## Examples

### Example 1

Input

```id="h4w5h6"
2
3
1 2 3
4
1 2 3 4
```

Explanation

For first test case:

```id="u9l2qs"
1 XOR 2 XOR 3 = 0
```

Since `n` is odd, choosing:

```id="od0o2m"
x = 0
```

works.

For second test case:

```id="jlwmrz"
1 XOR 2 XOR 3 XOR 4 = 4
```

`n` is even and total XOR is non-zero, so answer is impossible.

Output

```id="obw3ya"
0
-1
```

---

### Example 2

Input

```id="1y0um0"
1
4
5 5 5 5
```

Explanation

```id="fjlwm0"
5 XOR 5 XOR 5 XOR 5 = 0
```

So:

```id="44hljl"
x = 0
```

is valid.

Output

```id="nnhnqz"
0
```

---

### Example 3

Input

```id="7mjlwm"
1
5
7 1 2 3 4
```

Explanation

Total XOR:

```id="d9l8hd"
7 XOR 1 XOR 2 XOR 3 XOR 4 = 3
```

Since `n` is odd:

```id="qt3r9y"
x = 3
```

works.

Output

```id="8m9x8x"
3
```

## Approach

Bit Manipulation (XOR Property Observation)

## Intuition

Let:

```text id="a5qf7v"
res = a1 XOR a2 XOR ... XOR an
```

We need:

```text id="xov10s"
(a1 XOR x) XOR (a2 XOR x) ... XOR (an XOR x) = 0
```

Using XOR properties:

```text id="x2r5l1"
(a1 XOR a2 XOR ... XOR an) XOR (x repeated n times)
```

becomes:

```text id="yjdxkq"
res XOR x XOR x XOR ... (n times)
```

Key observations:

* If `n` is odd:

```text id="4s3rba"
x XOR x XOR x ... (odd times) = x
```

So:

```text id="2dht0k"
res XOR x = 0
x = res
```

* If `n` is even:

```text id="8k0m9j"
x XOR x ... (even times) = 0
```

Then condition becomes:

```text id="9b8mkg"
res = 0
```

If `res ≠ 0`, answer is impossible.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read `n`
  * Compute XOR of all elements → `res`
  * If `n` is odd:

    * Print `res`
  * Else:

    * If `res == 0` → print `0`
    * Else → print `-1`

## Visual Walkthrough

### Case 1

```id="n7w6jm"
Array = [1, 2, 3]
```

```id="g6mrxk"
1 XOR 2 XOR 3 = 0
n = 3 (odd)

x = 0
Result = 0
```

---

### Case 2

```id="fw4m9u"
Array = [1, 2, 3, 4]
```

```id="xj0j5q"
1 XOR 2 XOR 3 XOR 4 = 4
n = 4 (even)

res ≠ 0 → impossible
Answer = -1
```

---

### Case 3

```id="f1lhgs"
Array = [7, 1, 2, 3, 4]
```

```id="n4d0o6"
7 XOR 1 XOR 2 XOR 3 XOR 4 = 3
n = 5 (odd)

x = 3
```

## Complexity Analysis

### Time Complexity

**O(n) per test case**

Each element is processed once using XOR.

### Space Complexity

**O(1)**

Only constant extra variables are used.

## Solution Explanation

The solution relies on XOR properties:

* XORing a value an even number of times cancels out to `0`
* XORing a value an odd number of times leaves the value itself

By analyzing parity of `n`, we can directly determine whether a valid `x` exists and what its value should be.

## Full Solution

### C++ Implementation

```cpp id="jz3t0u"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        int n, num;

        // Stores XOR of all elements
        int res = 0;

        cin >> n;

        // Read array elements
        for(int i = 0; i < n; i++) {

            cin >> num;

            // Compute cumulative XOR
            res ^= num;
        }

        // If n is odd,
        // x = res works
        if(n & 1) {
            cout << res << '\n';
        }

        // If n is even and XOR already 0,
        // x = 0 works
        else if(res == 0) {
            cout << res << '\n';
        }

        // Otherwise impossible
        else {
            cout << "-1\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Array       | XOR Result | n Parity | Output |
| ----------- | ---------- | -------- | ------ |
| [1,2,3]     | 0          | Odd      | 0      |
| [1,2,3,4]   | 4          | Even     | -1     |
| [5,5,5,5]   | 0          | Even     | 0      |
| [7,1,2,3,4] | 3          | Odd      | 3      |

## Edge Cases to Consider

* Single element array
* All elements equal
* XOR already zero
* Large integer values

## Common Test Cases

* Odd-sized arrays
* Even-sized arrays with XOR = 0
* Even-sized arrays with XOR ≠ 0
* Arrays containing zeros

## Common Mistakes to Avoid

* Forgetting XOR cancellation property
* Confusing parity logic
* Using addition instead of XOR

## Interview Relevance

* Strong bit manipulation practice
* Tests XOR algebra understanding
* Common competitive programming pattern

## What This Problem Teaches

* Properties of XOR operations
* Impact of parity in bit manipulation
* Simplifying equations using XOR identities

## Key Takeaways

* XOR of identical values cancels out
* Odd and even occurrences behave differently
* Bitwise observations often simplify complex conditions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The implementation is straightforward once the XOR parity observation is identified.