# 994. Rotting Oranges

## Platform

LeetCode

## Problem Link

[994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)

## Problem Statement

You are given a 2D grid representing a box of oranges.

Each cell in the grid can have one of three values:

* `0` – empty cell
* `1` – fresh orange
* `2` – rotten orange

Every minute, any fresh orange that is **adjacent (up, down, left, or right)** to a rotten orange becomes rotten.

Return the **minimum number of minutes** that must elapse until **no cell has a fresh orange**.
If this is impossible, return `-1`.

## Input Format

* A 2D integer matrix `grid` of size `m × n`

  * `grid[i][j] ∈ {0, 1, 2}`

## Output Format

* An integer representing the minimum time required to rot all oranges
* Return `-1` if not all fresh oranges can be rotted

## Constraints

* `1 ≤ m, n ≤ 10`
* `grid[i][j]` is `0`, `1`, or `2`

## Examples

### Example 1

Input

```
grid = [
  [2,1,1],
  [1,1,0],
  [0,1,1]
]
```

Explanation

Minute-by-minute spread:

```
Minute 0: 2 1 1
          1 1 0
          0 1 1

Minute 1: 2 2 1
          2 1 0
          0 1 1

Minute 2: 2 2 2
          2 2 0
          0 1 1

Minute 3: 2 2 2
          2 2 0
          0 2 1

Minute 4: 2 2 2
          2 2 0
          0 2 2
```

Output

```
4
```

---

### Example 2

Input

```
grid = [
  [2,1,1],
  [0,1,1],
  [1,0,1]
]
```

Explanation

Some fresh oranges are isolated and never get infected.

Output

```
-1
```

---

### Example 3

Input

```
grid = [
  [0,2]
]
```

Explanation

There are no fresh oranges initially.

Output

```
0
```

## Approach

**Multi-source Breadth-First Search (BFS)**

## Intuition

All rotten oranges act as **simultaneous sources of infection**.

By pushing all rotten oranges into a queue initially and spreading rot level by level, each BFS layer naturally represents **one minute of time**.

If at the end any fresh orange remains, the task is impossible.

## Algorithm Steps

* Initialize a queue with all initially rotten oranges.
* Count the number of fresh oranges.
* If there are no fresh oranges, return `0`.
* Perform BFS level by level:

  * For each rotten orange in the current level:

    * Infect all valid adjacent fresh oranges.
    * Decrease the fresh count.
  * After processing one level, increment the timer.
* If fresh oranges remain, return `-1`; otherwise return the timer.

## Visual Walkthrough

### Case 1

```
Initial:
2 1 1
1 1 0
0 1 1
```

Rot spreads outward level by level from all `2`s simultaneously.

Each BFS level = **1 minute**

Final time = **4 minutes**

---

### Case 2

```
2 1 1
0 1 1
1 0 1
```

Some `1`s are unreachable → impossible

---

### Case 3

```
0 2
```

No fresh oranges → time = `0`

## Complexity Analysis

### Time Complexity

**O(m × n)**

Each cell is visited at most once during BFS.

### Space Complexity

**O(m × n)**

Queue may store all grid cells in the worst case.

## Solution Explanation

The solution treats all rotten oranges as BFS starting points.
By processing the grid level by level, it accurately simulates the passage of time.

The `fresh` counter ensures early termination and detects impossible cases efficiently.

## Full Solution

### C++ Implementation

```cpp
#include <vector>
#include <queue>
using namespace std;

class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {

        int m = grid.size();
        int n = grid[0].size();

        // Timer to track minutes
        int timer = 0;

        // Count of fresh oranges
        int fresh = 0;

        // Queue for BFS (row, column)
        queue<pair<int, int>> q;

        // Initialize queue with all rotten oranges
        // and count fresh oranges
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    fresh++;
                } else if (grid[i][j] == 2) {
                    q.push({i, j});
                }
            }
        }

        // If no fresh oranges exist
        if (fresh == 0) return 0;

        // BFS traversal
        while (!q.empty()) {

            int size = q.size();

            // Process one BFS level (one minute)
            while (size--) {

                auto p = q.front();
                q.pop();

                int r = p.first;
                int c = p.second;

                // Up
                if (r - 1 >= 0 && grid[r - 1][c] == 1) {
                    grid[r - 1][c] = 2;
                    q.push({r - 1, c});
                    fresh--;
                }

                // Right
                if (c + 1 < n && grid[r][c + 1] == 1) {
                    grid[r][c + 1] = 2;
                    q.push({r, c + 1});
                    fresh--;
                }

                // Down
                if (r + 1 < m && grid[r + 1][c] == 1) {
                    grid[r + 1][c] = 2;
                    q.push({r + 1, c});
                    fresh--;
                }

                // Left
                if (c - 1 >= 0 && grid[r][c - 1] == 1) {
                    grid[r][c - 1] = 2;
                    q.push({r, c - 1});
                    fresh--;
                }
            }

            // Increment time if infection continues
            if (!q.empty()) timer++;
        }

        // If fresh oranges remain, return -1
        return fresh ? -1 : timer;
    }
};
```

## Test Cases Analysis

| Grid Size | Fresh Exists | Reachable | Output |
| --------- | ------------ | --------- | ------ |
| 3 × 3     | Yes          | Yes       | 4      |
| 3 × 3     | Yes          | No        | -1     |
| 1 × 2     | No           | N/A       | 0      |
| 1 × 1     | Fresh only   | No        | -1     |

## Edge Cases to Consider

* No fresh oranges initially
* Fresh oranges completely isolated
* Single-cell grid
* All oranges already rotten

## Common Test Cases

* Fully connected grids
* Grids with obstacles (`0`)
* Multiple initial rotten sources

## Common Mistakes to Avoid

* Not using multi-source BFS
* Incorrect time increment logic
* Forgetting to check unreachable fresh oranges

## Interview Relevance

* Classic BFS grid problem
* Tests queue-based traversal
* Frequently asked in interviews

## What This Problem Teaches

* Multi-source BFS technique
* Level-order traversal for time simulation
* Grid boundary handling

## Key Takeaways

* BFS levels can model time
* Always track remaining targets
* Multi-source problems simplify with queues

## Problem Difficulty Analysis

This is a **Medium-level** problem.

It requires solid understanding of BFS and careful edge-case handling, making it a staple problem for technical interviews and competitive programming.