## 1527A. And Then There Were K

## Platform

Codeforces

## Problem Link

[And Then There Were K](https://codeforces.com/problemset/problem/1527/A)

## Problem Statement

Given an integer `n`, find the maximum possible integer `k` such that:

```text id="w8v5vx"
0 ≤ k < n
```

and

```text id="tf5a1x"
n & k = k
```

where `&` represents the bitwise AND operation.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains a single integer `n`.

## Output Format

* For each test case, print the maximum possible value of `k`.

## Constraints

* `1 ≤ t ≤ 10^4`
* `2 ≤ n ≤ 10^9`

## Examples

### Example 1

Input

```id="a5j5n6"
3
5
8
10
```

Explanation

For `n = 5`:

```id="u8r4gj"
Binary of 5 = 101
Maximum valid k = 3 → binary 011
101 & 011 = 001
```

For `n = 8`:

```id="o4e2ls"
Binary of 8 = 1000
Maximum valid k = 7 → binary 0111
```

For `n = 10`:

```id="d3n8tw"
Binary of 10 = 1010
Maximum valid k = 7 → binary 0111
```

Output

```id="e6h4sk"
3
7
7
```

---

### Example 2

Input

```id="o6g0gz"
2
2
3
```

Explanation

```id="y0q2gv"
n = 2 → answer = 1
n = 3 → answer = 1
```

Output

```id="l5p6zy"
1
1
```

---

### Example 3

Input

```id="r8s6x1"
1
17
```

Explanation

```id="n3z5fu"
17 in binary = 10001
Largest power of 2 less than 17 = 16
Answer = 16 - 1 = 15
```

Output

```id="m8g9kt"
15
```

## Approach

Bit Manipulation (Highest Power of Two Observation)

## Intuition

The maximum valid `k` is always:

```text id="z8v0cb"
(Highest power of 2 less than or equal to n) - 1
```

Why?

Numbers of the form:

```text id="r3m1kh"
2^x - 1
```

have all lower bits set:

```text id="o2t9zx"
1, 3, 7, 15, 31 ...
```

These values maximize `k` while ensuring:

```text id="h4q7dw"
k < n
```

and satisfy the required bitwise condition.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read integer `n`
  * Initialize `mask = 1`
  * Keep doubling `mask` until it becomes greater than `n`
  * Largest power of 2 ≤ `n` is:

```text id="x2l6wy"
mask >> 1
```

* Final answer:

```text id="q1o8yx"
(mask >> 1) - 1
```

* Print the result

## Visual Walkthrough

### Case 1

```id="t6o7vq"
n = 5
```

```id="j2n0ce"
mask progression:
1 → 2 → 4 → 8

8 > 5
Largest power of 2 ≤ 5 = 4

Answer = 4 - 1 = 3
```

---

### Case 2

```id="k1q5vf"
n = 8
```

```id="d8s9gv"
mask progression:
1 → 2 → 4 → 8 → 16

16 > 8
Largest power of 2 ≤ 8 = 8

Answer = 8 - 1 = 7
```

---

### Case 3

```id="v3z6qs"
n = 17
```

```id="g4m8db"
mask progression:
1 → 2 → 4 → 8 → 16 → 32

32 > 17
Largest power of 2 ≤ 17 = 16

Answer = 16 - 1 = 15
```

## Complexity Analysis

### Time Complexity

**O(log n)**

The loop repeatedly doubles `mask`, so it runs proportional to the number of bits in `n`.

### Space Complexity

**O(1)**

Only constant extra variables are used.

## Solution Explanation

The solution identifies the smallest power of 2 greater than `n`. The previous power of 2 is then used to construct the answer:

```text id="qqv4yt"
2^k - 1
```

This produces a number with all lower bits set, which is always the maximum valid answer.

## Full Solution

### C++ Implementation

```cpp id="n0r7pz"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input value
        int n;
        cin >> n;

        // Variable to store powers of 2
        int mask = 1;

        // Find first power of 2 greater than n
        while(n >= mask) {
            mask <<= 1;
        }

        // Largest power of 2 <= n is (mask >> 1)
        // Required answer is one less than that
        cout << (mask >> 1) - 1 << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n  | Largest Power of 2 ≤ n | Answer |
| -- | ---------------------- | ------ |
| 2  | 2                      | 1      |
| 5  | 4                      | 3      |
| 8  | 8                      | 7      |
| 10 | 8                      | 7      |
| 17 | 16                     | 15     |

## Edge Cases to Consider

* Minimum value of `n`
* `n` being a power of 2
* Very large values
* Consecutive numbers around powers of 2

## Common Test Cases

* `n = 2`
* `n = 2^k`
* `n = 2^k + 1`
* Random large integers

## Common Mistakes to Avoid

* Using `mask - 1` instead of `(mask >> 1) - 1`
* Incorrect loop condition
* Confusing highest power of 2 with nearest power of 2

## Interview Relevance

* Strong bit manipulation practice
* Tests binary representation understanding
* Common competitive programming pattern

## What This Problem Teaches

* Power-of-two properties
* Binary mask construction
* Efficient logarithmic computations

## Key Takeaways

* Numbers of form `2^k - 1` contain all lower bits set
* Bit manipulation often simplifies optimization problems
* Powers of two are extremely important in binary problems

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The main challenge is recognizing the relationship between the answer and powers of two. Once identified, the implementation becomes very straightforward.