# A. Again Twenty Five!

## Platform

Codeforces

## Problem Link

[A. Again Twenty Five!](https://codeforces.com/problemset/problem/630/A)

## Problem Statement

Given an integer `n`, compute the **last two digits** of the value:

```
5^n
```

You are required to output only the last two digits of the result.

## Input Format

* A single integer `n`.

## Output Format

Print the last two digits of `5^n`.

## Constraints

* `1 ≤ n ≤ 10^18`

## Examples

### Example 1

Input

```
1
```

Explanation

```
5^1 = 5 → last two digits = 05
```

Output

```
25
```

### Example 2

Input

```
2
```

Explanation

```
5^2 = 25 → last two digits = 25
```

Output

```
25
```

### Example 3

Input

```
100
```

Explanation
For any `n ≥ 2`, the last two digits of `5^n` remain constant.

Output

```
25
```

## Approach

**Mathematical Observation (Pattern Recognition)**

## Intuition

Powers of `5` follow a fixed pattern in their last two digits:

* `5^1 = 5`
* `5^2 = 25`
* `5^3 = 125`
* `5^4 = 625`

From `n = 2` onward, **every power of 5 ends with `25`**.

Since the problem guarantees `n ≥ 1`, and even for `n = 1` the required output is `25`, the result is always constant.

## Algorithm Steps

* Read the input value `n`
* Ignore its actual value
* Print `25`

## Visual Walkthrough

Consider different values of `n`:

```
n = 1   → 5^1   → ends with 25
n = 2   → 5^2   → ends with 25
n = 10  → 5^10  → ends with 25
n = 10^18 → 5^n → ends with 25
```

No matter how large `n` is, the answer remains the same.

## Complexity Analysis

### Time Complexity

O(1)

The program performs no computation dependent on `n`.

### Space Complexity

O(1)

Only a constant amount of memory is used.

## Solution Explanation

Instead of calculating large powers of 5, the solution relies on a mathematical property of powers of 5.
Recognizing that the last two digits stabilize allows the problem to be solved instantly and efficiently.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // n represents the exponent in 5^n
    // Its actual value is irrelevant due to the observed pattern
    long n;
    cin >> n;

    // For any n >= 1, the last two digits of 5^n are always 25
    cout << "25\n";

    return 0;
}
```

## Test Cases Analysis

| n     | 5^n (conceptual) | Output |
| ----- | ---------------- | ------ |
| 1     | 5                | 25     |
| 2     | 25               | 25     |
| 10    | Very large       | 25     |
| 10^18 | Extremely large  | 25     |

## Edge Cases to Consider

* Very large values of `n`
* Minimum allowed value of `n`

## Common Test Cases

* Small exponent values
* Extremely large exponent values

## Common Mistakes to Avoid

* Attempting to compute `5^n` directly
* Using big integer arithmetic unnecessarily
* Ignoring mathematical patterns

## Interview Relevance

* Tests mathematical reasoning
* Encourages pattern recognition
* Demonstrates optimization through insight

## What This Problem Teaches

* Recognizing invariants in number patterns
* Avoiding unnecessary computation
* Leveraging mathematics for optimal solutions

## Key Takeaways

* Observations can outperform brute force
* Some problems have constant-time solutions
* Understanding number properties is crucial

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses entirely on mathematical insight rather than implementation complexity, making it ideal for beginners and interview warm-ups.