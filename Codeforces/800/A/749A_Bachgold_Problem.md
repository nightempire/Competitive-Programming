# A. Bachgold Problem

## Platform

Codeforces

## Problem Link

[A. Bachgold Problem](https://codeforces.com/problemset/problem/749/A)

## Problem Statement

You are given an integer `n`.

Your task is to represent `n` as the **sum of the maximum possible number of prime numbers**, such that:

* All numbers used are **prime**
* The sum of these numbers is exactly `n`

You must output:

* The number of prime numbers used
* One valid representation of `n` using that many prime numbers

## Input Format

* A single integer `n`

## Output Format

* First line: an integer representing the count of prime numbers used
* Second line: the prime numbers whose sum equals `n`

## Constraints

* `2 ≤ n ≤ 10^5`

## Examples

### Example 1

Input

```
5
```

Explanation

To maximize the number of primes:

```
5 = 2 + 3
```

Output

```
2
2 3
```

### Example 2

Input

```
6
```

Explanation

```
6 = 2 + 2 + 2
```

Output

```
3
2 2 2
```

## Approach

Greedy decomposition using the smallest prime number.

## Intuition

To maximize the number of prime numbers in the sum:

* Always use the **smallest prime**, which is `2`
* Using smaller primes allows more terms in the sum

However:

* If `n` is odd, using only `2`s will leave a remainder of `1`, which is not prime
* To fix this, replace one `2` with a `3`

This guarantees both correctness and the maximum count.

## Algorithm Steps

* Read integer `n`
* Compute `size = n / 2`
* Print `size` as the number of primes
* Print `size - 1` times the value `2`
* If `n` is odd, print `3` as the last number
* Otherwise, print `2` as the last number

## Visual Walkthrough

### Test Case 1

Input:

```
n = 7
```

Computation:

```
7 / 2 = 3
```

Representation:

```
2 + 2 + 3 = 7
```

Output:

```
3
2 2 3
```

---

### Test Case 2

Input:

```
n = 8
```

Computation:

```
8 / 2 = 4
```

Representation:

```
2 + 2 + 2 + 2 = 8
```

Output:

```
4
2 2 2 2
```

---

### Test Case 3

Input:

```
n = 3
```

Computation:

```
3 / 2 = 1
```

Representation:

```
3
```

Output:

```
1
3
```

## Complexity Analysis

### Time Complexity

O(n)

The loop prints up to `n / 2` values.

### Space Complexity

O(1)

Only constant extra variables are used (output excluded).

## Solution Explanation

The solution greedily uses the smallest prime number `2` to maximize the number of terms.
When `n` is odd, replacing one `2` with a `3` ensures the sum remains valid and prime-only.

This method is simple, optimal, and fully aligned with the problem requirements.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Read the integer n
    int n;
    cin >> n;

    // Maximum number of primes is n / 2
    int size = n / 2;

    // Print the number of primes used
    cout << size << '\n';

    // Print size - 1 times the prime number 2
    for (int i = 0; i < size - 1; i++)
        cout << "2 ";

    // If n is odd, end with 3; otherwise end with 2
    cout << (n & 1 ? "3" : "2");

    return 0;
}
```

## Test Cases Analysis

| n | Output Count | Representation | Reason         |
| - | ------------ | -------------- | -------------- |
| 2 | 1            | 2              | Smallest prime |
| 3 | 1            | 3              | Odd prime      |
| 5 | 2            | 2 3            | Odd handling   |
| 6 | 3            | 2 2 2          | All 2s         |
| 7 | 3            | 2 2 3          | Max count      |

## Edge Cases to Consider

* `n = 2`
* `n = 3`
* Very large values of `n`

## Common Test Cases

* Even numbers
* Odd numbers
* Small boundary inputs

## Common Mistakes to Avoid

* Using composite numbers
* Not handling odd `n` correctly
* Trying unnecessary prime generation

## Interview Relevance

* Tests greedy problem-solving
* Evaluates understanding of prime properties
* Common constructive algorithm problem

## What This Problem Teaches

* Greedy strategies for maximization
* Leveraging mathematical observations
* Writing concise constructive solutions

## Key Takeaways

* Smallest units often maximize count
* Special cases (odd values) must be handled explicitly
* Simplicity leads to optimal solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on mathematical reasoning and constructive logic rather than complex algorithms.