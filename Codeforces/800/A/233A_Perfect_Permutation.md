# A_Perfect_Permutation

## Platform

Codeforces

## Problem Link

[A. Perfect Permutation](https://codeforces.com/problemset/problem/233/A)

---

## Problem Statement

Given a positive integer `n`, construct a permutation `p` of size `n` such that:

```id="g5m6ad"
p[i] ≠ i   for all 1 ≤ i ≤ n
```

In other words, no element should remain in its original position.
Such a permutation is called a **derangement**.

If it is impossible to construct such a permutation, print:

```id="r6a4nm"
-1
```

Otherwise, print any valid permutation.

---

## Input Format

* A single integer `n`.

---

## Output Format

* If no valid permutation exists, print `-1`.
* Otherwise, print `n` integers representing a valid permutation.

---

## Constraints

* `1 ≤ n ≤ 100`

---

## Examples

### Example 1

Input

```id="wh3c4p"
4
```

Output

```id="rb53yx"
2 1 4 3
```

Explanation:

* p[1] = 2 ≠ 1
* p[2] = 1 ≠ 2
* p[3] = 4 ≠ 3
* p[4] = 3 ≠ 4

Valid derangement.

---

### Example 2

Input

```id="wq0f4k"
3
```

Output

```id="q3p9wa"
-1
```

Explanation:

For odd `n`, it is impossible to rearrange all elements so that no element remains in its original position using the required structure.

---

## Approach (Algorithm Type)

**Pairwise Swapping (Constructive Greedy Approach)**

---

## Intuition

We need:

```id="n1d6yz"
p[i] ≠ i
```

The simplest construction:

* Swap adjacent pairs.

For example:

```id="m1v3tg"
1 2 3 4 → 2 1 4 3
```

This ensures:

* Every element moves from its original index.
* No fixed points exist.

However, this works only if `n` is even.

If `n` is odd:

* One element will remain unmatched.
* That element cannot be swapped.
* Therefore, no valid permutation exists.

---

## Why It Fails for Odd n

For odd `n`:

* Pairwise swapping leaves one element at the end.
* That element remains in its original position.
* So at least one fixed point exists.

Thus:

```id="c5kht2"
If n is odd → print -1
```

---

## Algorithm Steps

* Read integer `n`.
* If `n` is odd:

  * Print `-1`.
* Else:

  * For `i = 1` to `n` in steps of 2:

    * Print `i+1` and `i`.

---

## Visual Walkthrough

### Test Case 1

Input:

```id="zsk8vd"
n = 6
```

Pairs:

```id="nmz6fi"
(1,2) → 2 1
(3,4) → 4 3
(5,6) → 6 5
```

Result:

```id="oj8o1m"
2 1 4 3 6 5
```

Check:

| i | p[i] | Valid? |
| - | ---- | ------ |
| 1 | 2    | ✓      |
| 2 | 1    | ✓      |
| 3 | 4    | ✓      |
| 4 | 3    | ✓      |
| 5 | 6    | ✓      |
| 6 | 5    | ✓      |

---

### Test Case 2

Input:

```id="h2ur9x"
n = 5
```

One element left after pairing:

```id="7bsy2l"
(1,2)
(3,4)
5 → remains fixed
```

Invalid → Output `-1`

---

## Complexity Analysis

### Time Complexity

* Single loop from `1` to `n`
* Each element processed once

```id="9rt1fg"
O(n)
```

---

### Space Complexity

```id="wz4wlc"
O(1)
```

No extra storage used.

---

## Solution Explanation

The solution checks whether `n` is even.

If even:

* It prints elements in swapped pairs.
* Ensures no element stays in original position.

If odd:

* Prints `-1` because constructing such a permutation is impossible.

This constructive method guarantees correctness.

---

## Full Solution

### C++ Implementation

```cpp id="g3zq1b"
#include<iostream>
using namespace std;

int main() {

    int n;
    cin >> n;

    // If n is odd, impossible to form perfect permutation
    if(n & 1) {
        cout << "-1\n";
        return 0;
    }

    // Swap adjacent elements
    for(int i = 1; i <= n; i += 2) {
        cout << i + 1 << ' ' << i << ' ';
    }

    cout << '\n';

    return 0;
}
```

---

## Test Cases Analysis

| n | Output Example |
| - | -------------- |
| 1 | -1             |
| 2 | 2 1            |
| 3 | -1             |
| 4 | 2 1 4 3        |
| 6 | 2 1 4 3 6 5    |

---

## Edge Cases to Consider

* `n = 1`
* `n = 2`
* Large even values
* Maximum constraint

---

## Common Test Cases

* Small odd number
* Small even number
* Larger even number
* Boundary value `n = 100`

---

## Common Mistakes to Avoid

* Forgetting odd check
* Incorrect loop increment
* Printing extra space (though harmless)

---

## Interview Relevance

* Tests permutation construction logic
* Demonstrates greedy construction
* Reinforces understanding of derangements

---

## What This Problem Teaches

* Constructive algorithm techniques
* Observing feasibility conditions
* Handling parity constraints

---

## Key Takeaways

* Pairwise swapping removes fixed points.
* Odd-length derangement is impossible in this simple construction.
* Always check feasibility before constructing.

---

## Problem Difficulty Analysis

This is an **Easy-level** Codeforces problem.

It primarily tests constructive thinking and parity reasoning, making it ideal for beginners and competitive programming practice.