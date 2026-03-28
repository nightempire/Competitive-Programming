## Platform

Codeforces

## Problem Link

[A. Maximum in Table](https://codeforces.com/problemset/problem/509/A)

---

## Problem Statement

You are given an integer `n`.

Construct an `n × n` table such that:

* The first row and the first column are filled with `1`
* Every other cell `(i, j)` contains the sum of:

  * The value above it → `arr[i-1][j]`
  * The value to the left → `arr[i][j-1]`

Your task is to compute and print the value at the **bottom-right corner**, i.e., `arr[n-1][n-1]`.

---

## Input Format

* A single integer `n`

---

## Output Format

* Print a single integer — the value at position `(n-1, n-1)`

---

## Constraints

* `1 ≤ n ≤ 10`

---

## Examples

### Example 1

Input

```id="gkq9l2"
1
```

Explanation

Only one cell exists:

```
1
```

Output

```id="p0u5hl"
1
```

---

### Example 2

Input

```id="fdmlci"
2
```

Explanation

```
1 1
1 2
```

Bottom-right = `2`

Output

```id="6v3t2u"
2
```

---

### Example 3

Input

```id="y3g3se"
4
```

Explanation

Construct table:

```
1  1  1  1
1  2  3  4
1  3  6 10
1  4 10 20
```

Bottom-right = `20`

Output

```id="q1gmyk"
20
```

---

## Approach

Dynamic Programming (2D DP table construction)

---

## Intuition

Each cell depends on two previously computed values:

```
arr[i][j] = arr[i-1][j] + arr[i][j-1]
```

This resembles **Pascal’s Triangle in 2D form**.

Key observation:

* The table builds cumulative paths
* Final value equals number of ways to reach `(n-1, n-1)` from `(0,0)`

---

## Algorithm Steps

* Read integer `n`
* Create a 2D array `arr[n][n]`
* Iterate through all cells:

  * If `i == 0` or `j == 0`:

    * Set value to `1`
  * Else:

    * Compute:

      ```
      arr[i][j] = arr[i-1][j] + arr[i][j-1]
      ```
* Print `arr[n-1][n-1]`

---

## Visual Walkthrough

### Case 1: `n = 3`

```
Step-by-step:

1 1 1
1 ? ?
1 ? ?

Fill:

arr[1][1] = 1+1 = 2
arr[1][2] = 2+1 = 3
arr[2][1] = 1+2 = 3
arr[2][2] = 3+3 = 6
```

Final:

```
1 1 1
1 2 3
1 3 6
```

---

### Case 2: `n = 4`

```
1  1  1  1
1  2  3  4
1  3  6 10
1  4 10 20
```

---

### Case 3: `n = 2`

```
1 1
1 2
```

---

## Complexity Analysis

### Time Complexity

O(n²)

* We fill each cell once

---

### Space Complexity

O(n²)

* 2D array is used

---

## Solution Explanation

The problem follows a classic dynamic programming pattern:

* Base case: first row and column = 1
* Transition: each cell is sum of top and left

This builds the table incrementally and guarantees correct computation.

---

## Full Solution

### C++ Implementation

```cpp id="5m3k6m"
#include<iostream>
using namespace std;

int main() {

    // Size of the table
    int n;
    cin >> n;

    // Declare 2D array
    int arr[n][n];

    // Fill the table
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < n; j++) {

            // Base case: first row or column
            if(i == 0 || j == 0) {
                arr[i][j] = 1;
            }

            // Recurrence relation
            else {
                arr[i][j] = arr[i - 1][j] + arr[i][j - 1];
            }
        }
    }

    // Output the bottom-right value
    cout << arr[n - 1][n - 1];
}
```

---

## Test Cases Analysis

| n | Table Size | Bottom-Right Value |
| - | ---------- | ------------------ |
| 1 | 1×1        | 1                  |
| 2 | 2×2        | 2                  |
| 3 | 3×3        | 6                  |
| 4 | 4×4        | 20                 |
| 5 | 5×5        | 70                 |

---

## Edge Cases to Consider

* `n = 1` (minimum case)
* Maximum `n = 10`
* Symmetry of table

---

## Common Test Cases

* `n = 1` → 1
* `n = 2` → 2
* `n = 3` → 6
* `n = 5` → 70

---

## Common Mistakes to Avoid

* Incorrect indexing
* Forgetting base case initialization
* Accessing invalid indices

---

## Interview Relevance

* Classic DP problem
* Grid path counting
* Foundation for combinatorics problems

---

## What This Problem Teaches

* Building DP tables
* Understanding recurrence relations
* Connection to Pascal’s Triangle

---

## Key Takeaways

* DP simplifies repeated computations
* Always define base cases clearly
* Grid problems often map to combinatorics

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Basic dynamic programming
* Table construction
* Recurrence relations