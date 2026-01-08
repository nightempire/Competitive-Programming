# A_Design_Tutorial_Learn_from_Math

## Platform

Codeforces

## Problem Link

[A. Design Tutorial: Learn from Math](https://codeforces.com/problemset/problem/472/A)

## Problem Statement

You are given an integer `n`.

Your task is to represent `n` as the sum of **two composite numbers**.
A composite number is a positive integer greater than `1` that is **not prime**.

It is guaranteed that such a representation always exists for the given constraints.

## Input Format

* A single integer `n`

## Output Format

Print two composite integers whose sum is equal to `n`.

The two numbers should be printed on the same line, separated by a space.

## Constraints

* `12 ≤ n ≤ 10^9`
* A valid answer is guaranteed to exist

## Examples

### Example 1

Input

```
12
```

Explanation

* `4` and `8` are both composite
* `4 + 8 = 12`

Output

```
4 8
```

### Example 2

Input

```
15
```

Explanation

* `9` and `6` are both composite
* `9 + 6 = 15`

Output

```
9 6
```

## Approach (Algorithm Name / Type)

**Parity-Based Constant Decomposition**

This approach uses predefined composite numbers and leverages the parity of `n` to ensure correctness.

## Intuition

Some small composite numbers are always available:

* `4` is composite
* `9` is composite

Observations:

* If `n` is even:

  * `n - 4` is also even and ≥ 8
  * Any even number ≥ 4 is composite
* If `n` is odd:

  * `n - 9` is even and ≥ 6
  * Any even number ≥ 4 is composite

Thus, choosing `(4, n - 4)` for even `n` and `(9, n - 9)` for odd `n` always produces two composite numbers.

## Algorithm Steps

* Read integer `n`.
* If `n` is odd:

  * Output `9` and `n - 9`
* Otherwise:

  * Output `4` and `n - 4`

## Visual Walkthrough

### Case 1: `n` is Even

Input:

```
n = 20
```

Decomposition:

```
4 + 16 = 20
```

Both numbers:

```
4 → composite
16 → composite
```

---

### Case 2: `n` is Odd

Input:

```
n = 21
```

Decomposition:

```
9 + 12 = 21
```

Both numbers:

```
9 → composite
12 → composite
```

---

### Case 3: Minimum Value

Input:

```
n = 12
```

Decomposition:

```
4 + 8 = 12
```

## Complexity Analysis

### Time Complexity

**O(1)**

Only a single conditional check is performed.

### Space Complexity

**O(1)**

No extra memory is used.

## Solution Explanation

The solution avoids checking for primality or iterating over possible values.

By using fixed composite numbers (`4` and `9`) and adjusting based on the parity of `n`, the algorithm guarantees that both output numbers are composite and sum to `n`.

This makes the solution extremely efficient and mathematically sound.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Read the input number
    int n;
    cin >> n;

    // If n is odd, use 9 (composite) and n - 9
    if (n & 1) {
        cout << 9 << " " << n - 9;
    }
    // If n is even, use 4 (composite) and n - 4
    else {
        cout << 4 << " " << n - 4;
    }

    return 0;
}
```

## Test Cases Analysis

| Input `n` | Output Pair | Reasoning                |
| --------: | ----------: | ------------------------ |
|        12 |       `4 8` | Both composite, sum = 12 |
|        15 |       `9 6` | Both composite, sum = 15 |
|        20 |      `4 16` | Even decomposition       |
|        21 |      `9 12` | Odd decomposition        |

## Edge Cases to Consider

* Minimum allowed value (`n = 12`)
* Very large values of `n`
* Odd and even values of `n`

## Common Test Cases

* Small even numbers
* Small odd numbers
* Large random values

## Common Mistakes to Avoid

* Using prime numbers like `2` or `3`
* Forgetting that both numbers must be composite
* Adding unnecessary primality checks

## Interview Relevance

* Demonstrates mathematical reasoning
* Tests understanding of number properties
* Common example of constructive problem-solving

## What This Problem Teaches

* Leveraging mathematical guarantees
* Using parity effectively
* Designing constant-time solutions

## Key Takeaways

* Composite numbers can be guaranteed using small constants
* Mathematical insight often replaces brute force
* Elegant solutions are both fast and reliable

## Problem Difficulty Analysis

This is an **Easy-level** problem.

Although it appears mathematical, the logic is straightforward once key observations are made, making it suitable for beginners and interview preparation.