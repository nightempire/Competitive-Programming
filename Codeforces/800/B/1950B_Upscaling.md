## Platform

Codeforces

## Problem Link

[B. Upscaling](https://codeforces.com/problemset/problem/1950/B)

---

## Problem Statement

You are given an integer `n`.

Your task is to generate a **2n × 2n grid pattern** using the characters:

* `#`
* `.`

The pattern must follow these rules:

* Each cell in an `n × n` conceptual grid expands into a **2 × 2 block**
* The pattern alternates like a chessboard:

  * Even cells → filled with `##`
  * Odd cells → filled with `..`

---

## Input Format

* The first line contains an integer `t` — number of test cases
* Each test case contains a single integer `n`

---

## Output Format

For each test case:

* Print a `2n × 2n` grid satisfying the pattern rules

---

## Constraints

* `1 ≤ t ≤ 20`
* `1 ≤ n ≤ 20`

---

## Examples

### Example 1

Input

```
1
2
```

Explanation

We construct a `4 × 4` grid:

* Each cell becomes a `2 × 2` block
* Alternating pattern is maintained

Output

```
##..
##..
..##
..##
```

---

### Example 2

Input

```
1
3
```

Explanation

Grid size = `6 × 6`

Output

```
##..##
##..##
..##..
..##..
##..##
##..##
```

---

### Example 3

Input

```
1
1
```

Output

```
##
##
```

---

## Approach

Pattern generation using nested loops (grid expansion simulation)

---

## Intuition

Instead of explicitly creating an `n × n` grid and then expanding it, we directly construct the `2n × 2n` grid.

Key idea:

* Each row in the original grid is printed **twice**
* Each column in the original grid is printed as **two characters (`##` or `..`)**
* Pattern alternates based on parity

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `n`
  * Loop `i` from `0` to `n-1`:

    * Repeat twice (to expand rows):

      * Loop `k` from `i` to `i + n - 1`:

        * If `k` is even → print `"##"`
        * Else → print `".."`
      * Move to next line

---

## Visual Walkthrough

### Case 1: `n = 2`

Conceptual grid:

```
# .
. #
```

Expanded:

```
## ..
## ..
.. ##
.. ##
```

---

### Case 2: `n = 3`

Conceptual:

```
# . #
. # .
# . #
```

Expanded:

```
## .. ##
## .. ##
.. ## ..
.. ## ..
## .. ##
## .. ##
```

---

### Case 3: `n = 1`

Conceptual:

```
#
```

Expanded:

```
##
##
```

---

## Complexity Analysis

### Time Complexity

O(n²) per test case

* We generate a grid of size `2n × 2n`

---

### Space Complexity

O(1)

* No additional memory used beyond printing

---

## Solution Explanation

The solution cleverly avoids storing the grid and directly prints the pattern.

* The outer loop controls rows
* Each row is duplicated
* The inner loop determines whether to print `"##"` or `".."` based on parity

The use of `(i + offset)` ensures alternating pattern across rows.

---

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t, n;
    cin >> t;

    // Process each test case
    while(t--) {

        // Input size
        cin >> n;

        // Loop through each row of conceptual grid
        for(int i = 0; i < n; i++) {

            // Define range for alternating pattern
            int m = n + i;

            // Each row is printed twice (vertical expansion)
            for(int j = 0; j < 2; j++) {

                // Generate columns
                for(int k = i; k < m; k++) {

                    // Alternate pattern using parity
                    if(k & 1) {
                        cout << "..";  // Odd → dots
                    } else {
                        cout << "##";  // Even → hashes
                    }
                }

                // Move to next line
                cout << '\n';
            }
        }
    }

    return 0;
}
```

---

## Test Cases Analysis

| n | Grid Size | Pattern Type       | Output Shape |
| - | --------- | ------------------ | ------------ |
| 1 | 2×2       | Single block       | ## / ##      |
| 2 | 4×4       | Alternating blocks | Checker      |
| 3 | 6×6       | Extended pattern   | Checker      |

---

## Edge Cases to Consider

* `n = 1`
* Maximum `n = 20`
* Multiple test cases

---

## Common Test Cases

* `n = 1` → smallest grid
* `n = 2` → basic alternating
* `n = 5` → larger pattern

---

## Common Mistakes to Avoid

* Forgetting to print each row twice
* Incorrect parity logic
* Wrong loop ranges

---

## Interview Relevance

* Pattern generation problems
* Nested loop control
* Visualization of grid transformations

---

## What This Problem Teaches

* Translating conceptual grids into expanded outputs
* Efficient printing without extra storage
* Pattern recognition using parity

---

## Key Takeaways

* Expansion problems can often be solved directly during output
* Parity is powerful in pattern generation
* Avoid unnecessary data structures

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Pattern construction
* Loop control
* Logical thinking