# Flip Square Submatrix Vertically

## Platform

LeetCode

## Problem Link

[3643. Flip Square Submatrix Vertically](https://leetcode.com/problems/flip-square-submatrix-vertically)

## Problem Statement

You are given a 2D matrix `grid` of size `m × n`.

You are also given three integers:

* `x` — starting row index
* `y` — starting column index
* `k` — size of the square submatrix

Your task is to **flip the `k × k` submatrix vertically**.

### Vertical Flip Definition

A vertical flip means:

* Reverse the rows inside the submatrix
* Columns remain unchanged

## Input Format

* A 2D integer matrix `grid`
* Integers `x`, `y`, `k`

## Output Format

Return the modified matrix after flipping the specified submatrix.

## Constraints

* `1 ≤ m, n ≤ 100`
* `0 ≤ x < m`
* `0 ≤ y < n`
* `1 ≤ k ≤ min(m, n)`
* The submatrix `(x, y)` to `(x+k-1, y+k-1)` is valid

## Examples

### Example 1

Input

```
grid = [
 [1, 2, 3],
 [4, 5, 6],
 [7, 8, 9]
]
x = 0, y = 0, k = 3
```

Explanation

Submatrix:

```
1 2 3
4 5 6
7 8 9
```

After vertical flip:

```
7 8 9
4 5 6
1 2 3
```

Output

```
[
 [7, 8, 9],
 [4, 5, 6],
 [1, 2, 3]
]
```

---

### Example 2

Input

```
grid = [
 [1, 2, 3, 4],
 [5, 6, 7, 8],
 [9,10,11,12],
 [13,14,15,16]
]
x = 1, y = 1, k = 2
```

Submatrix:

```
6 7
10 11
```

After flip:

```
10 11
6 7
```

Output

```
[
 [1, 2, 3, 4],
 [5,10,11, 8],
 [9, 6, 7,12],
 [13,14,15,16]
]
```

---

### Example 3

Input

```
grid = [
 [1,2],
 [3,4]
]
x = 0, y = 0, k = 1
```

Explanation

Single element → no change.

Output

```
[
 [1,2],
 [3,4]
]
```

## Approach

Two-Pointer Row Swapping (In-Place Matrix Manipulation)

## Intuition

A vertical flip means:

* Swap the **top row** of the submatrix with the **bottom row**
* Move inward until the middle is reached

For a submatrix:

```
row x       ↔ row x+k-1
row x+1     ↔ row x+k-2
...
```

Columns remain fixed.

So for each column `j` in `[y, y+k-1]`, swap elements:

```
grid[top][j] ↔ grid[bottom][j]
```

## Algorithm Steps

* Compute:

  ```
  bottom = x + k - 1
  ```
* Iterate rows from:

  ```
  i = x to (x + bottom) / 2
  ```
* For each row `i`, swap with:

  ```
  opposite_row = x + bottom - i
  ```
* For each column `j` from `y` to `y + k - 1`:

  * Swap:

    ```
    grid[i][j] ↔ grid[opposite_row][j]
    ```

## Visual Walkthrough

### Example

```
grid:
1 2 3
4 5 6
7 8 9
```

Swap steps:

```
Row 0 ↔ Row 2
```

After swap:

```
7 8 9
4 5 6
1 2 3
```

---

### Partial Submatrix Example

```
Original:
5 6 7 8
9 10 11 12
```

Swap rows:

```
5 6 7 8   ↔   9 10 11 12
```

Result:

```
9 10 11 12
5 6 7 8
```

## Complexity Analysis

### Time Complexity

```
O(k²)
```

We process all elements inside the `k × k` submatrix.

### Space Complexity

```
O(1)
```

In-place swapping is used.

## Solution Explanation

The solution:

* Computes the bottom boundary of the submatrix
* Iterates from top to middle
* Swaps corresponding rows element-wise

The formula:

```cpp
m + x - i
```

correctly finds the mirrored row index.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    vector<vector<int>> reverseSubmatrix(vector<vector<int>>& grid, int x, int y, int k) {

        // Bottom row of the submatrix
        int m = x + k - 1;

        // Rightmost column of the submatrix
        int n = y + k - 1;

        // Iterate from top row to middle row of submatrix
        for(int i = x; i <= (m + x) / 2; i++) {

            // Traverse all columns in submatrix
            for(int j = y; j <= n; j++) {

                // Swap current row with corresponding bottom row
                int temp = grid[i][j];

                // Mirror row index: m + x - i
                grid[i][j] = grid[m + x - i][j];
                grid[m + x - i][j] = temp;
            }
        }

        return grid;
    }
};
```

## Test Cases Analysis

| Submatrix Size | Operation   | Result        |
| -------------- | ----------- | ------------- |
| 3×3            | Full flip   | Rows reversed |
| 2×2            | Swap 2 rows | Correct       |
| 1×1            | No change   | Same          |

## Edge Cases to Consider

* `k = 1` (no change)
* Submatrix at boundary
* Entire grid selected
* Odd `k` (middle row remains unchanged)

## Common Test Cases

```
3x3 full matrix
2x2 submatrix
1x1 submatrix
large grid
```

## Common Mistakes to Avoid

* Incorrect mirror index calculation
* Off-by-one errors in loop bounds
* Swapping columns instead of rows
* Not limiting to submatrix boundaries

## Interview Relevance

* Tests matrix manipulation
* Demonstrates in-place transformations
* Reinforces indexing logic

## What This Problem Teaches

* Submatrix handling
* Two-pointer technique in 2D arrays
* Careful boundary management

## Key Takeaways

* Vertical flip = row reversal within submatrix
* Use symmetric index mapping
* In-place operations optimize space

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It primarily tests understanding of matrix indexing and basic in-place transformations, making it straightforward once the flipping concept is clear.