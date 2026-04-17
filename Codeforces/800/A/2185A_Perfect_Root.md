## Platform

Codeforces

## Problem Link

[A. Perfect Root](https://codeforces.com/problemset/problem/2185/A)

---

## Problem Statement

You are given an integer `n`.

Your task is to construct a permutation of integers from `1` to `n`.

For this problem, **any valid permutation** is acceptable.

---

## Input Format

* The first line contains an integer `t` — number of test cases
* For each test case:

  * A single integer `n`

---

## Output Format

For each test case:

* Print a permutation of integers from `1` to `n`

---

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 100`

---

## Examples

### Example 1

Input

```id="m2k9zp"
3
1
3
5
```

Output

```id="p7x3ql"
1
1 2 3
1 2 3 4 5
```

---

### Example 2

Input

```id="t5v8mr"
2
4
2
```

Output

```id="z9k2px"
1 2 3 4
1 2
```

---

### Example 3

Input

```id="r6m3qt"
1
6
```

Output

```id="k4p8xn"
1 2 3 4 5 6
```

---

## Approach

Direct construction (identity permutation)

---

## Intuition

A permutation is simply:

```text id="a2k9vp"
A rearrangement of numbers from 1 to n
```

Since the problem does **not impose additional constraints**, the simplest valid permutation is:

```text id="z7m3qx"
1 2 3 ... n
```

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `n`
  * Print numbers from `1` to `n`

---

## Visual Walkthrough

### Case 1: `n = 3`

```text id="k8p2mv"
Permutation: 1 2 3
```

---

### Case 2: `n = 5`

```text id="t3m7xp"
Permutation: 1 2 3 4 5
```

---

### Case 3: `n = 1`

```text id="z5k1rp"
Permutation: 1
```

---

## Complexity Analysis

### Time Complexity

O(n) per test case

* Printing `n` numbers

---

### Space Complexity

O(1)

* No extra space used

---

## Solution Explanation

The solution simply outputs the identity permutation:

* This satisfies the definition of a permutation
* No further constraints need to be handled

---

## Full Solution

### C++ Implementation

```cpp id="v3k8zp"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input n
        int n;
        cin >> n;

        // Print permutation from 1 to n
        for(int i = 1; i <= n; i++) {
            cout << i << ' ';
        }

        cout << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| n | Output    |
| - | --------- |
| 1 | 1         |
| 2 | 1 2       |
| 3 | 1 2 3     |
| 5 | 1 2 3 4 5 |

---

## Edge Cases to Consider

* `n = 1`
* Small values
* Multiple test cases

---

## Common Test Cases

* `n = 1`
* `n = 2`
* `n = 10`

---

## Common Mistakes to Avoid

* Printing numbers outside range
* Missing newline after each test case
* Misinterpreting permutation requirement

---

## Interview Relevance

* Understanding permutations
* Basic loop construction
* Output formatting

---

## What This Problem Teaches

* Simplicity in problem solving
* Recognizing when constraints are minimal
* Avoiding overcomplication

---

## Key Takeaways

* Identity permutation is always valid
* Not all problems require complex logic
* Read constraints carefully

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Basic programming constructs
* Output generation
* Understanding definitions