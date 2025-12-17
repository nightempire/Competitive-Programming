Below is a **professional, publication-ready Markdown document** generated strictly from the solution you provided, following your required structure and conventions.

---

# Max Area of Island

## Platform

**LeetCode**

## Problem Link

[695. Max Area of Island](https://leetcode.com/problems/max-area-of-island/)

---

## Problem Statement

You are given a 2D grid of integers where:

* `1` represents **land**
* `0` represents **water**

An **island** is a group of connected land cells (`1`) connected **horizontally or vertically** (not diagonally).

The **area of an island** is the number of land cells in that island.

Your task is to return the **maximum area** of any island in the grid.
If there are no islands, return `0`.

---

## Input Format

* A 2D integer matrix `grid` of size `m × n`
* Each cell contains either `0` or `1`

---

## Output Format

* An integer representing the **maximum area of an island**

---

## Constraints

* `1 ≤ m, n ≤ 50`
* `grid[i][j] ∈ {0, 1}`
* The grid is rectangular

---

## Example

### Example 1

**Input**

```
grid = [
  [0,0,1,0,0,0,0,1,0,0,0,0,0],
  [0,0,0,0,0,0,0,1,1,1,0,0,0],
  [0,1,1,0,1,0,0,0,0,0,0,0,0],
  [0,1,0,0,1,1,0,0,1,0,1,0,0],
  [0,1,0,0,1,1,0,0,1,1,1,0,0],
  [0,0,0,0,0,0,0,0,0,0,1,0,0],
  [0,0,0,0,0,0,0,1,1,1,0,0,0],
  [0,0,0,0,0,0,0,1,1,0,0,0,0]
]
```

**Output**

```
6
```

**Explanation**

* The largest connected group of `1`s contains **6 cells**
* That group forms the maximum island area

---

## Approach: Depth-First Search (DFS)

### Core Idea

* Traverse the grid cell by cell.
* When a land cell (`1`) is found:

  * Use **DFS** to explore the entire island.
  * Count the number of connected land cells.
* Track and update the **maximum island area** encountered.

---

## Algorithm

1. Initialize `maxArea = 0`
2. Traverse each cell in the grid
3. When a land cell (`1`) is found:

   * Call DFS to calculate the area of the island
   * Update `maxArea` with the maximum value
4. Continue until the grid is fully processed
5. Return `maxArea`

---

## Complexity Analysis

* **Time Complexity**: `O(m × n)`
  Each cell is visited once at most.
* **Space Complexity**: `O(m × n)` (worst case)
  Due to recursive DFS stack when the grid is filled with land.

---

## Solution Explanation (Step-by-Step)

1. **Grid Traversal**

   * Nested loops iterate over every cell.

2. **Island Detection**

   * A value of `1` indicates unvisited land.
   * DFS is initiated to compute the island’s area.

3. **DFS Exploration**

   * The DFS:

     * Marks the current cell as visited (`1 → 0`)
     * Recursively explores:

       * Up
       * Right
       * Down
       * Left
   * Each valid land cell contributes `+1` to the area.

4. **Area Calculation**

   * DFS returns the total number of connected land cells.
   * The maximum area is updated accordingly.

5. **Final Result**

   * The largest area found is returned.

---

## Full Solution

```java
class Solution {

    // DFS returns the area of the current island
    public static int dfs(int[][] grid, int row, int col) {

        // Boundary condition: outside the grid
        if (row < 0 || col < 0 || row >= grid.length || col >= grid[0].length)
            return 0;

        // Process only land cells
        if (grid[row][col] == 1) {

            // Mark current cell as visited
            grid[row][col] = 0;

            // Count current cell + all connected neighbors
            return 1
                    + dfs(grid, row - 1, col) // up
                    + dfs(grid, row, col + 1) // right
                    + dfs(grid, row + 1, col) // down
                    + dfs(grid, row, col - 1); // left
        }

        // Water or already visited cell
        return 0;
    }

    // Returns the maximum island area
    public int maxAreaOfIsland(int[][] grid) {
        int max = 0;

        // Traverse the grid
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {

                // If land is found, compute island area
                if (grid[i][j] == 1) {
                    max = Math.max(max, dfs(grid, i, j));
                }
            }
        }

        return max;
    }
}
```

---

## Key Insights

* This is a **grid-based connected components** problem.
* DFS naturally fits area calculation problems.
* In-place modification avoids extra memory for visited tracking.
* Returning values from DFS simplifies area aggregation.

---

## Common Mistakes to Avoid

1. Forgetting to mark visited cells
2. Missing boundary checks in DFS
3. Counting diagonally connected cells (not allowed)
4. Not resetting or tracking maximum properly
5. Stack overflow risk on very large grids (iterative DFS/BFS can be alternatives)

---

## Interview Relevance

This problem evaluates:

* DFS recursion mastery
* Grid traversal logic
* In-place state modification
* Accurate area computation

It is a **frequently asked LeetCode problem** and a natural extension of *Number of Islands*.