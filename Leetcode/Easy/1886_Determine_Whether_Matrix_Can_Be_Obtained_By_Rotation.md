# Determine Whether Matrix Can Be Obtained By Rotation

## Platform

LeetCode

## Problem Link

[1886. Determine Whether Matrix Can Be Obtained By Rotation](https://leetcode.com/problems/determine-whether-matrix-can-be-obtained-by-rotation)

## Problem Statement

You are given two `n × n` binary matrices:

* `mat`
* `target`

You can rotate `mat` in-place by **90 degrees clockwise** any number of times (0, 1, 2, or 3 times).

Your task is to determine whether `mat` can be made equal to `target` after some number of rotations.

Return:

* `true` if possible
* `false` otherwise

## Input Format

* A 2D vector `mat`
* A 2D vector `target`

## Output Format

Return a boolean value.

## Constraints

* `1 ≤ n ≤ 10`
* `mat[i][j], target[i][j] ∈ {0,1}`

## Examples

### Example 1

Input

```id="kvh72a"
mat =
[ [0,1],
  [1,0] ]

target =
[ [1,0],
  [0,1] ]
```

Explanation

Rotate `mat` by 90°:

```id="qgxbxg"
[ [1,0],
  [0,1] ]
```

Matches target → `true`

---

### Example 2

Input

```id="g4e1s9"
mat =
[ [0,1],
  [1,1] ]

target =
[ [1,0],
  [0,1] ]
```

No rotation matches.

Output

```id="u0lb3b"
false
```

---

### Example 3

Input

```id="2k6s1d"
mat =
[ [1,1,0],
  [0,1,1],
  [1,0,1] ]

target =
[ [1,0,1],
  [1,1,0],
  [0,1,1] ]
```

After rotation, matrices match → `true`

## Approach

Simultaneous Rotation Check (Mathematical Mapping)

## Intuition

Instead of physically rotating the matrix multiple times, we can **check all 4 possible rotations simultaneously**.

For any element `(i, j)` in `mat`, the corresponding positions in `target` after rotations are:

### 0° Rotation

```id="rdaz0z"
(i, j)
```

### 90° Rotation

```id="nyxx55"
(j, n - i - 1)
```

### 180° Rotation

```id="fjc0dn"
(n - i - 1, n - j - 1)
```

### 270° Rotation

```id="r6yn1b"
(n - j - 1, i)
```

We check all four possibilities in one pass.

## Algorithm Steps

* Initialize a boolean array:

```id="4yqb7d"
flag[4] = {true, true, true, true}
```

* Traverse all elements `(i, j)`:

  * Compare with each rotation:

    * If mismatch → mark corresponding flag as `false`

* Return:

```id="m2rdcb"
flag[0] || flag[1] || flag[2] || flag[3]
```

## Visual Walkthrough

### Original Matrix

```id="9kp1ah"
1 2
3 4
```

### Rotations

**90°**

```id="8lr6yx"
3 1
4 2
```

**180°**

```id="sdprpf"
4 3
2 1
```

**270°**

```id="9icd12"
2 4
1 3
```

---

### Mapping Example

For `(i, j) = (0, 1)`:

| Rotation | Position  |
| -------- | --------- |
| 0°       | (0,1)     |
| 90°      | (1,n-1)   |
| 180°     | (n-1,n-2) |
| 270°     | (n-2,0)   |

## Complexity Analysis

### Time Complexity

```id="cfkjy7"
O(n²)
```

We traverse the matrix once.

### Space Complexity

```id="5nnv0j"
O(1)
```

Only constant extra space is used.

## Solution Explanation

The solution avoids explicit matrix rotation.

Instead, it:

* Uses index transformations to simulate rotations
* Checks all rotations in a **single traversal**
* Uses flags to track validity

This is efficient and avoids redundant work.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    bool findRotation(vector<vector<int>>& mat, vector<vector<int>>& target) {

        // Flags for 4 rotations: 0°, 90°, 180°, 270°
        bool flag[4] = {true, true, true, true};

        int n = mat.size();

        // Traverse matrix
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {

                // Check 0° rotation
                if(mat[i][j] != target[i][j])
                    flag[0] = false;

                // Check 90° rotation
                if(mat[i][j] != target[j][n - i - 1])
                    flag[1] = false;

                // Check 180° rotation
                if(mat[i][j] != target[n - i - 1][n - j - 1])
                    flag[2] = false;

                // Check 270° rotation
                if(mat[i][j] != target[n - j - 1][i])
                    flag[3] = false;
            }
        }

        // If any rotation matches
        return flag[0] || flag[1] || flag[2] || flag[3];
    }
};
```

## Test Cases Analysis

| Case        | Rotation Match | Result |
| ----------- | -------------- | ------ |
| Exact match | 0°             | true   |
| 90° match   | Yes            | true   |
| 180° match  | Yes            | true   |
| No match    | None           | false  |

## Edge Cases to Consider

* `n = 1`
* Matrices already equal
* All elements same
* No rotation works

## Common Test Cases

```id="j9q2rg"
[[1]] → [[1]]
[[0,1],[1,0]] → [[1,0],[0,1]]
[[1,1],[1,1]] → [[1,1],[1,1]]
```

## Common Mistakes to Avoid

* Incorrect rotation index mapping
* Performing actual rotations unnecessarily
* Forgetting one of the 4 rotation cases

## Interview Relevance

* Tests matrix transformation skills
* Demonstrates optimization (avoid recomputation)
* Common 2D array manipulation problem

## What This Problem Teaches

* Rotation mapping in matrices
* Efficient checking using index transformations
* Avoiding redundant operations

## Key Takeaways

* Matrix rotation can be handled mathematically
* Check all transformations in one pass
* Use symmetry to simplify logic

## Problem Difficulty Analysis

This is an **Easy-to-Medium level** problem.

While the implementation is straightforward, deriving correct index mappings for all rotations is the key challenge.