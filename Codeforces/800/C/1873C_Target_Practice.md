# C_Target_Practice

## Platform

Codeforces

## Problem Link

[C. Target Practice](https://codeforces.com/problemset/problem/1873/C)

## Problem Statement

You are given a **10 × 10 grid** representing a target board.

* Each cell contains either:

  * `'X'` → a successful hit
  * `'.'` → an empty cell
* The board consists of **concentric square layers**, similar to a dartboard.

Each layer has a score:

* Center (innermost layer) → **5 points**
* Moving outward, scores decrease by 1
* Outermost layer → **1 point**

Your task is to **calculate the total score** of all `'X'` cells for each test case.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * 10 lines follow
  * Each line contains a string of length 10 consisting of characters `'X'` or `'.'`

## Output Format

* For each test case, output a single integer representing the total score.

## Constraints

* `1 ≤ t ≤ 1000`
* Grid size is always `10 × 10`
* Each character is either `'X'` or `'.'`

## Examples

### Example 1

Input

```
1
..........
..........
....X.....
..........
..........
..........
..........
..........
..........
..........
```

Explanation

* The `'X'` is located in layer 3
* Score = 3

Output

```
3
```

---

### Example 2

Input

```
1
XXXXXXXXXX
XXXXXXXXXX
XXXXXXXXXX
XXXXXXXXXX
XXXXXXXXXX
XXXXXXXXXX
XXXXXXXXXX
XXXXXXXXXX
XXXXXXXXXX
XXXXXXXXXX
```

Explanation

* All cells are filled
* Sum of all layer scores is calculated

Output

```
220
```

## Approach – 1

**Layer-Based Conditional Mapping**

## Intuition (Approach 1)

Each cell belongs to a specific square layer based on its row and column indices.

By checking index ranges manually, we can directly assign the correct score to each `'X'`.

The closer the cell is to the center, the higher the score.

## Algorithm Steps (Approach 1)

* Read number of test cases `t`.
* For each test case:

  * Initialize `score = 0`.
  * Loop through each row `i` from `0` to `9`.
  * Read the row string.
  * Loop through each column `j` from `0` to `9`.
  * If the cell contains `'X'`:

    * Check which layer it belongs to using index ranges.
    * Add the corresponding score.
* Print the total score.

## Visual Walkthrough (Approach 1)

### Cell at `(4, 4)`

```
i = 4, j = 4
```

* Lies in the center square
* Score = 5

---

### Cell at `(1, 8)`

```
i = 1, j = 8
```

* Lies in the second outermost layer
* Score = 2

---

### Cell at `(0, 0)`

```
i = 0, j = 0
```

* Outermost layer
* Score = 1

## Complexity Analysis (Approach 1)

### Time Complexity

**O(1) per test case**

* Grid size is constant (`10 × 10`).

### Space Complexity

**O(1)**

* Only integer variables are used.

## Solution Explanation (Approach 1)

The solution explicitly checks index boundaries to determine which square layer a cell belongs to.
This approach is intuitive and easy to understand but slightly verbose due to multiple conditional checks.

## Full Solution (Approach 1)

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int score = 0;

        // Iterate over the 10x10 grid
        for (int i = 0; i < 10; i++) {
            string s;
            cin >> s;

            for (int j = 0; j < 10; j++) {

                // Check if the cell contains a hit
                if (s[j] == 'X') {

                    // Determine the layer using index ranges
                    if (i >= 4 && i <= 5 && j >= 4 && j <= 5)
                        score += 5;
                    else if (i >= 3 && i <= 6 && j >= 3 && j <= 6)
                        score += 4;
                    else if (i >= 2 && i <= 7 && j >= 2 && j <= 7)
                        score += 3;
                    else if (i >= 1 && i <= 8 && j >= 1 && j <= 8)
                        score += 2;
                    else
                        score += 1;
                }
            }
        }

        cout << score << '\n';
    }

    return 0;
}
```

---

## Approach – 2

**Mathematical Layer Calculation**

## Intuition (Approach 2)

Instead of manually checking ranges, the layer of a cell can be computed mathematically.

The layer number is the **minimum distance from the cell to any border** of the grid.

This produces a clean and concise solution.

## Algorithm Steps (Approach 2)

* Read number of test cases `t`.
* For each test case:

  * Initialize `score = 0`.
  * Loop through each cell `(i, j)`.
  * If the cell contains `'X'`:

    * Compute

      ```
      layer = min(min(i, j), min(9 - i, 9 - j))
      ```
    * Add `layer + 1` to the score.
* Print the total score.

## Visual Walkthrough (Approach 2)

### Cell `(0, 0)`

```
Distances → top = 0, left = 0, bottom = 9, right = 9
layer = 0
score = 1
```

---

### Cell `(4, 4)`

```
Distances → top = 4, left = 4, bottom = 5, right = 5
layer = 4
score = 5
```

---

### Cell `(2, 7)`

```
Distances → top = 2, left = 7, bottom = 7, right = 2
layer = 2
score = 3
```

## Complexity Analysis (Approach 2)

### Time Complexity

**O(1) per test case**

* Fixed grid size.

### Space Complexity

**O(1)**

* Constant auxiliary space.

## Solution Explanation (Approach 2)

This approach converts a geometric problem into a mathematical one.
By computing the minimum distance from the borders, the layer and score are obtained directly, resulting in cleaner and more maintainable code.

## Full Solution (Approach 2)

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int score = 0;

        // Iterate through the grid
        for (int i = 0; i < 10; i++) {
            string s;
            cin >> s;

            for (int j = 0; j < 10; j++) {

                // Check for a hit
                if (s[j] == 'X') {

                    // Calculate the layer using minimum distance to borders
                    int layer = min(min(i, j), min(9 - i, 9 - j));

                    // Add the score for this layer
                    score += layer + 1;
                }
            }
        }

        cout << score << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Scenario          | Description         | Expected Result     |
| ----------------- | ------------------- | ------------------- |
| Single hit center | One `'X'` at center | 5                   |
| Single hit border | One `'X'` at corner | 1                   |
| Multiple hits     | Mixed layers        | Sum of layer scores |
| Full grid         | All `'X'`           | Maximum score       |

## Edge Cases to Consider

* All cells are `'.'`
* Only border cells contain `'X'`
* Only center cells contain `'X'`

## Common Test Cases

* Sparse grid with few hits
* Dense grid with many hits
* Multiple test cases input

## Common Mistakes to Avoid

* Incorrect layer calculation
* Off-by-one errors in indices
* Forgetting to reset score per test case

## Interview Relevance

* Tests 2D grid traversal
* Demonstrates geometric reasoning
* Highlights mathematical optimization

## What This Problem Teaches

* Translating geometry into logic
* Using symmetry in grids
* Writing clean and efficient solutions

## Key Takeaways

* Mathematical formulations reduce conditional complexity
* Grid problems often hide simple patterns
* Clean logic improves maintainability

## Problem Difficulty Analysis

This is an **Easy-to-Medium** level problem.
It focuses on observation and clean implementation rather than heavy computation.