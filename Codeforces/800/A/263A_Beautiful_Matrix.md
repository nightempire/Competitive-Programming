# A. Beautiful Matrix

## Platform

Codeforces

## Problem Link

[A. Beautiful Matrix](https://codeforces.com/problemset/problem/263/A)

## Problem Statement

You are given a `5 × 5` matrix containing only `0`s and exactly **one** `1`.

The matrix is considered **beautiful** if the `1` is located at the **center position** of the matrix, that is at row `3`, column `3` (1-based indexing).

In one move, you are allowed to **swap two adjacent rows** or **swap two adjacent columns**.

Determine the **minimum number of moves** required to make the matrix beautiful.

## Input Format

* Five lines follow.
* Each line contains five integers (`0` or `1`), representing the matrix.

## Output Format

* Print a single integer representing the minimum number of moves needed.

## Constraints

* Matrix size is fixed at `5 × 5`
* Exactly one element in the matrix is `1`
* All other elements are `0`

## Examples

### Example 1

Input

```
0 0 0 0 0
0 0 0 0 0
0 0 1 0 0
0 0 0 0 0
0 0 0 0 0
```

Explanation
The `1` is already at the center position.

Output

```
0
```

---

### Example 2

Input

```
0 0 0 0 0
0 0 0 0 0
0 0 0 0 1
0 0 0 0 0
0 0 0 0 0
```

Explanation
The `1` is at position `(3, 5)` (1-based).
Moves required:

* Shift left by `2` columns

Output

```
2
```

---

## Approach

Manhattan distance calculation.

## Intuition

* The final target position of `1` is the center of the matrix.
* Swapping adjacent rows or columns moves the `1` **one step** vertically or horizontally.
* The minimum number of moves equals the **sum of vertical and horizontal distances** from the current position to the center.

This is exactly the Manhattan distance between the current position and the center.

## Algorithm Steps

* Read the `5 × 5` matrix
* Identify the row and column indices of the value `1`
* Compute:

  * Vertical distance to row `2` (0-based center)
  * Horizontal distance to column `2`
* Sum both distances
* Output the result

## Visual Walkthrough

Matrix indices (0-based):

```
Center → (2, 2)
```

If `1` is at `(i, j)`:

Moves required:

```
|2 - i| + |2 - j|
```

Each unit represents a single row or column swap.

## Complexity Analysis

### Time Complexity

O(1)
The matrix size is constant (`5 × 5`).

### Space Complexity

O(1)
Only fixed-size variables are used.

## Solution Explanation

The solution scans the matrix to locate the position of the `1`.
Once found, it calculates how far the `1` is from the center both vertically and horizontally.

Because each move shifts the `1` by one position, the sum of these distances gives the minimum number of moves required.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // 5x5 matrix to store input values
    int mat[5][5];

    // Variables to store the position of '1'
    int oneRowIdx = -1;
    int oneColIdx = -1;

    // Read the matrix
    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 5; j++) {

            // Read each cell value
            cin >> mat[i][j];

            // If the value is 1, store its position
            if (mat[i][j]) {
                oneRowIdx = i;
                oneColIdx = j;
            }
        }
    }

    // Center of the matrix in 0-based indexing is (2, 2)
    // Calculate Manhattan distance to the center
    cout << abs(2 - oneRowIdx) + abs(2 - oneColIdx);

    return 0;
}
```

## Test Cases Analysis

| Position of `1` (0-based) | Calculation       | Output |
| ------------------------- | ----------------- | ------ |
| (2, 2)                    | |2-2| + |2-2| = 0 | 0      |
| (0, 0)                    | 2 + 2             | 4      |
| (4, 4)                    | 2 + 2             | 4      |
| (1, 3)                    | 1 + 1             | 2      |

## Edge Cases to Consider

* `1` already at the center
* `1` at a corner position
* `1` on the edge but not in a corner

## Common Test Cases

* Center placement
* Corner placement
* Edge placement

## Common Mistakes to Avoid

* Using 1-based indexing internally
* Forgetting to take absolute values
* Misidentifying the center position

## Interview Relevance

* Tests understanding of grid traversal
* Demonstrates Manhattan distance usage
* Common warm-up problem in interviews

## What This Problem Teaches

* Translating movement constraints into distance formulas
* Efficient handling of fixed-size matrices
* Recognizing when brute force is unnecessary

## Key Takeaways

* Manhattan distance is ideal for grid movement problems
* Fixed-size constraints simplify complexity analysis
* Clear indexing prevents off-by-one errors

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on logical reasoning and distance calculation rather than algorithmic complexity, making it ideal for beginners and interview preparation.