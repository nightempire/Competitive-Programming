## Platform

LeetCode

## Problem Link

[2946. Matrix Similarity After Cyclic Shifts](https://leetcode.com/problems/matrix-similarity-after-cyclic-shifts)

---

## Problem Statement

You are given a 2D integer matrix `mat` of size `m × n` and an integer `k`.

Define an operation where each row of the matrix is cyclically shifted:

* **Even-indexed rows (0-based)** → shift **left by `k`**
* **Odd-indexed rows** → shift **right by `k`**

Your task is to determine whether, after performing these operations, the matrix remains **unchanged**.

Return `true` if the matrix is the same after the shifts, otherwise return `false`.

---

## Input Format

* A 2D integer array `mat` of size `m × n`
* An integer `k`

---

## Output Format

* Return `true` if the matrix remains unchanged
* Otherwise return `false`

---

## Constraints

* `1 ≤ m, n ≤ 100`
* `1 ≤ mat[i][j] ≤ 1000`
* `0 ≤ k ≤ 10^9`

---

## Examples

### Example 1

Input

```
mat = [[1,2,1,2],
       [3,4,3,4]]
k = 2
```

Explanation

* Row 0 (even) → left shift by 2 → `[1,2,1,2]`
* Row 1 (odd) → right shift by 2 → `[3,4,3,4]`

Matrix remains same

Output

```
true
```

---

### Example 2

Input

```
mat = [[1,2,3],
       [4,5,6]]
k = 1
```

Explanation

* Row 0 → `[2,3,1]`
* Row 1 → `[6,4,5]`

Matrix changes

Output

```
false
```

---

### Example 3

Input

```
mat = [[7,7,7],
       [7,7,7]]
k = 5
```

Explanation

* All elements identical → remains same after any shift

Output

```
true
```

---

## Approach

Modulo-based cyclic comparison (row-wise invariance check)

---

## Intuition

Instead of actually performing shifts, we can **directly verify if each element maps to itself after shifting**.

Key observation:

* Left shift by `k` → index becomes `(j + k) % n`
* Right shift by `k` → index becomes `(j - k + n) % n`

If the matrix is unchanged, then:

```
mat[i][j] == shifted_position_value
```

for all elements.

---

## Algorithm Steps

* Compute `k = k % n` to avoid redundant shifts
* For each row `i`:

  * For each column `j`:

    * If `i` is even:

      * Compare `mat[i][j]` with `mat[i][(j + k) % n]`
    * If `i` is odd:

      * Compare `mat[i][j]` with `mat[i][(j - k + n) % n]`
    * If mismatch found → return `false`
* If all checks pass → return `true`

---

## Visual Walkthrough

### Case 1

```
Row: [1,2,1,2], k = 2

Shifted (left):
[1,2,1,2]

All positions match → valid
```

---

### Case 2

```
Row: [1,2,3], k = 1

Shifted:
[2,3,1]

Mismatch at index 0 → invalid
```

---

### Case 3

```
Row: [7,7,7]

Any shift → [7,7,7]

Always valid
```

---

## Complexity Analysis

### Time Complexity

O(m × n)

* Each element is checked exactly once

---

### Space Complexity

O(1)

* No extra space used

---

## Solution Explanation

The solution avoids explicitly shifting rows, which would cost extra time and space.

Instead, it leverages **modular arithmetic** to compute the expected position after shifting and compares directly.

If all elements remain consistent with their shifted counterparts, the matrix is considered unchanged.

---

## Full Solution

### C++ Implementation

```cpp
#include <vector>
using namespace std;

class Solution {
public:
    bool areSimilar(vector<vector<int>>& mat, int k) {

        // Number of rows and columns
        int m = mat.size(), n = mat[0].size();

        // Reduce k to avoid unnecessary full rotations
        k %= n;

        // Traverse each row
        for(int i = 0; i < m; i++) {

            // Traverse each column
            for(int j = 0; j < n; j++) {

                // For even rows → left shift
                if(i % 2 == 0) {

                    // Compare with shifted position
                    if(mat[i][j] != mat[i][(j + k) % n]) {
                        return false;
                    }

                } else {

                    // For odd rows → right shift
                    if(mat[i][j] != mat[i][(j - k + n) % n]) {
                        return false;
                    }
                }
            }
        }

        // If all elements match
        return true;
    }
};
```

---

## Test Cases Analysis

| Matrix        | k | Result | Reason                    |
| ------------- | - | ------ | ------------------------- |
| [[1,2,1,2]]   | 2 | true   | periodic pattern          |
| [[1,2,3]]     | 1 | false  | mismatch after shift      |
| [[7,7,7]]     | 5 | true   | all same values           |
| [[1],[2],[3]] | 3 | true   | single column → no change |

---

## Edge Cases to Consider

* `k = 0` → no shift
* `n = 1` → no visible change
* Large `k` values
* Rows with identical elements

---

## Common Test Cases

* Single row matrix
* Single column matrix
* All elements same
* Alternating patterns

---

## Common Mistakes to Avoid

* Forgetting `k %= n`
* Using same shift direction for all rows
* Actually modifying matrix unnecessarily

---

## Interview Relevance

* Tests modular arithmetic usage
* Matrix traversal skills
* Optimization by avoiding simulation

---

## What This Problem Teaches

* Cyclic shifts using modulo
* Pattern invariance checking
* Efficient simulation avoidance

---

## Key Takeaways

* Always reduce large shifts using modulo
* Avoid actual transformations when verification suffices
* Direction-based logic is crucial

---

## Problem Difficulty Analysis

This is an **Easy to Medium-level** problem.

It involves:

* Matrix traversal
* Index manipulation
* Modular arithmetic reasoning