# A_Panoramix_s_Prediction

## Platform

Codeforces

## Problem Link

[A. Panoramix’s Prediction](https://codeforces.com/problemset/problem/80/A)

## Problem Statement

Panoramix wants to test your knowledge of **prime numbers**.

You are given two integers `n` and `m`.

Your task is to determine whether `m` is the **next prime number immediately after `n`**.

* If `m` is the next prime after `n`, print `YES`
* Otherwise, print `NO`

## Input Format

* A single line containing two integers `n` and `m`

## Output Format

Print `YES` if `m` is the next prime after `n`, otherwise print `NO`.

## Constraints

* `2 ≤ n < m ≤ 50`
* `n` is guaranteed to be a prime number

## Examples

### Example 1

Input

```
3 5
```

Explanation

Prime numbers sequence:

```
2, 3, 5, 7, 11, ...
```

The next prime after `3` is `5`, which matches `m`.

Output

```
YES
```

### Example 2

Input

```
7 11
```

Explanation

The next prime after `7` is `11`.

Output

```
YES
```

### Example 3

Input

```
7 13
```

Explanation

The next prime after `7` is `11`, not `13`.

Output

```
NO
```

## Approach (Algorithm Name / Type)

**Precomputed Prime Lookup**

## Intuition

The constraints are very small, and all possible prime numbers up to `50` are known.

Instead of checking primality dynamically, we can store all required prime numbers in a fixed array and simply verify whether `m` directly follows `n` in the prime sequence.

This makes the solution both simple and efficient.

## Algorithm Steps

* Store all prime numbers up to `50` in an array
* Read integers `n` and `m`
* Find the index of `n` in the prime array
* Check whether the next prime in the array is equal to `m`
* Print `YES` if it matches, otherwise print `NO`

## Visual Walkthrough

### Test Case 1

Input

```
n = 3, m = 5
```

Prime array

```
[2, 3, 5, 7, 11, ...]
```

Index of `3` → `1`
Next prime → `5`

Result

```
YES
```

---

### Test Case 2

Input

```
n = 7, m = 13
```

Index of `7` → `3`
Next prime → `11`

Comparison

```
11 ≠ 13
```

Result

```
NO
```

---

### Test Case 3

Input

```
n = 43, m = 47
```

Index of `43` → `11`
Next prime → `47`

Result

```
YES
```

## Complexity Analysis

### Time Complexity

**O(1)**
The prime array has a fixed size, and lookup takes constant time.

### Space Complexity

**O(1)**
Only a small fixed array of prime numbers is used.

## Solution Explanation

The solution leverages the fact that all required prime numbers are within a small, fixed range.

By precomputing and storing these primes, the problem reduces to a simple index comparison.
This avoids unnecessary prime-checking logic and keeps the implementation concise and reliable.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Precomputed list of prime numbers up to 50
    int primes[] = {
        2, 3, 5, 7, 11,
        13, 17, 19, 23, 29,
        31, 37, 41, 43, 47
    };

    int n, m;
    int idx = 0;

    // Read input values
    cin >> n >> m;

    // Find the index of n in the prime array
    while (primes[idx++] != n);

    // Check if the next prime is equal to m
    if (primes[idx] == m) {
        cout << "YES\n";
    } else {
        cout << "NO\n";
    }

    return 0;
}
```

## Test Cases Analysis

| n  | m  | Next Prime After n | Output |
| -- | -- | ------------------ | ------ |
| 3  | 5  | 5                  | YES    |
| 7  | 11 | 11                 | YES    |
| 7  | 13 | 11                 | NO     |
| 43 | 47 | 47                 | YES    |
| 29 | 31 | 31                 | YES    |

## Edge Cases to Consider

* `n` is the largest prime less than `50`
* `m` is not a prime
* `m` skips one or more primes after `n`

## Common Test Cases

* Consecutive primes
* Non-consecutive primes
* Boundary prime values

## Common Mistakes to Avoid

* Checking only if both numbers are prime
* Ignoring the order of primes
* Implementing unnecessary primality tests

## Interview Relevance

* Tests understanding of prime number sequences
* Demonstrates optimization using precomputation
* Evaluates logical indexing skills

## What This Problem Teaches

* Leveraging constraints to simplify solutions
* Using lookup tables effectively
* Avoiding overengineering for small input sizes

## Key Takeaways

* Precomputation can drastically simplify logic
* Always consider problem constraints before designing algorithms
* Sequential properties of numbers can often be exploited

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It requires basic understanding of prime numbers and sequence ordering, making it suitable for beginners and early interview preparation.