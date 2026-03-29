## Platform

Codeforces

## Problem Link

[A. Special Permutation](https://codeforces.com/problemset/problem/1454/A)

---

## Problem Statement

You are given an integer `n`.

Your task is to construct a **permutation of numbers from `1` to `n`** such that:

* For every index `i` (1-based), the element at position `i` is **not equal to `i`**

In other words, construct a permutation where **no element is in its original position** (a derangement-like condition).

---

## Input Format

* The first line contains an integer `t` — number of test cases
* For each test case:

  * A single integer `n`

---

## Output Format

For each test case:

* Print a permutation of integers from `1` to `n` satisfying the condition

---

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n ≤ 100`

---

## Examples

### Example 1

Input

```id="gk2t7w"
3
2
3
4
```

Explanation

* `n = 2` → swap both elements
* `n = 3` → rotate left
* `n = 4` → rotate left

Output

```id="y4k3dp"
2 1
2 3 1
2 3 4 1
```

---

### Example 2

Input

```id="7wq2n5"
2
5
1
```

Explanation

* `n = 5` → rotate
* `n = 1` → no valid permutation exists, but problem allows output (edge case)

Output

```id="e2v8r9"
2 3 4 5 1
1
```

---

### Example 3

Input

```id="b6m3xa"
1
6
```

Output

```id="r3k9zn"
2 3 4 5 6 1
```

---

## Approach

Cyclic left rotation (simple derangement construction)

---

## Intuition

A simple and optimal way to ensure:

```id="3zsm7x"
p[i] ≠ i
```

is to **shift all elements by one position**:

* Move `1` to the end
* Shift all others left

Result:

```id="8zn9ft"
[2, 3, 4, ..., n, 1]
```

This guarantees:

* Every element moves away from its original position
* No index `i` contains value `i`

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `n`
  * Print numbers from `2` to `n`
  * Print `1` at the end

---

## Visual Walkthrough

### Case 1: `n = 3`

```id="d7l8wf"
Original: 1 2 3
Shifted : 2 3 1

Check:
pos1 → 2 ✔
pos2 → 3 ✔
pos3 → 1 ✔
```

---

### Case 2: `n = 4`

```id="t8v6xp"
Original: 1 2 3 4
Shifted : 2 3 4 1
```

---

### Case 3: `n = 5`

```id="6s4e9z"
Original: 1 2 3 4 5
Shifted : 2 3 4 5 1
```

---

## Complexity Analysis

### Time Complexity

O(n) per test case

* Printing `n` elements

---

### Space Complexity

O(1)

* No additional memory used

---

## Solution Explanation

The solution constructs a valid permutation using a **cyclic rotation**.

This avoids complex derangement logic and guarantees correctness with minimal effort.

Since each number is shifted forward, no element remains in its original position.

---

## Full Solution

### C++ Implementation

```cpp id="3l6q2p"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t, n;
    cin >> t;

    // Process each test case
    while(t--) {

        // Read n
        cin >> n;

        // Print numbers from 2 to n
        for(int i = 2; i <= n; i++) {
            cout << i << ' ';
        }

        // Print 1 at the end
        cout << "1\n";
    }

    return 0;
}
```

---

## Test Cases Analysis

| n | Output    | Valid |
| - | --------- | ----- |
| 2 | 2 1       | ✔     |
| 3 | 2 3 1     | ✔     |
| 4 | 2 3 4 1   | ✔     |
| 5 | 2 3 4 5 1 | ✔     |

---

## Edge Cases to Consider

* `n = 1` → no valid derangement (but accepted in problem)
* Small values (`n = 2`)
* Larger values

---

## Common Test Cases

* `n = 1` → 1
* `n = 2` → 2 1
* `n = 3` → 2 3 1

---

## Common Mistakes to Avoid

* Trying complex derangement algorithms unnecessarily
* Forgetting to print `1` at the end
* Incorrect loop boundaries

---

## Interview Relevance

* Understanding permutations
* Constructive algorithms
* Greedy/simple transformations

---

## What This Problem Teaches

* Simple constructions can solve complex-looking constraints
* Recognizing patterns like cyclic shifts
* Avoiding overengineering

---

## Key Takeaways

* Rotation ensures no fixed points
* Always look for simple patterns first
* Constructive problems often have elegant solutions

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Permutation construction
* Logical reasoning
* Pattern recognition