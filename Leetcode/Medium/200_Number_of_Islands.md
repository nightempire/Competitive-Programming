Below is a **professionally structured Markdown document** for the given solution.
It follows the exact format and rigor you specified and is suitable for notes, GitHub, or documentation.

---

# Number of Islands

## Platform

**LeetCode**

## Problem Link

[200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

---

## Problem Statement

Given a 2D grid consisting of characters `'1'` (land) and `'0'` (water), determine the total number of **islands**.

An island is formed by connecting adjacent lands **horizontally or vertically**. You may assume all four edges of the grid are surrounded by water.

---

## Input Format

* A 2D character matrix `grid` of size `m × n`
* Each cell contains either:

  * `'1'` → land
  * `'0'` → water

---

## Output Format

* Return an integer representing the **number of islands** present in the grid.

---

## Constraints

* `1 ≤ m, n ≤ 300`
* `grid[i][j]` is either `'0'` or `'1'`
* Grid is rectangular

---

## Example

### Example 1

**Input**

```
grid = [
  ['1','1','1','1','0'],
  ['1','1','0','1','0'],
  ['1','1','0','0','0'],
  ['0','0','0','0','0']
]
```

**Output**

```
1
```

**Explanation**

* All `'1'` cells are connected, forming a single island.

---

### Example 2

**Input**

```
grid = [
  ['1','1','0','0','0'],
  ['1','1','0','0','0'],
  ['0','0','1','0','0'],
  ['0','0','0','1','1']
]
```

**Output**

```
3
```

**Explanation**

* There are three separate land regions, each counted as one island.

---

## Approach: Depth-First Search (DFS)

### Key Idea

* Traverse the grid cell by cell.
* When a land cell (`'1'`) is found:

  * Increment the island count.
  * Perform a **DFS** to mark all connected land cells as visited.
* Marking visited cells prevents recounting the same island.

---

## Algorithm

1. Initialize a counter `count = 0`.
2. Iterate through every cell in the grid.
3. If the current cell is `'1'`:

   * Call DFS to explore and mark the entire island.
   * Increment `count`.
4. Continue until all cells are processed.
5. Return `count`.

---

## Complexity Analysis

* **Time Complexity**: `O(m × n)`
  Each cell is visited at most once.
* **Space Complexity**: `O(m × n)` (worst case)
  Due to recursion stack in DFS when the grid is filled with land.

---

## Solution Explanation (Step-by-Step)

1. **Grid Traversal**

   * Two nested loops scan every cell in the grid.

2. **Island Detection**

   * A cell containing `'1'` represents unvisited land.
   * This indicates the discovery of a new island.

3. **Depth-First Search**

   * DFS explores all four directions:

     * Up
     * Right
     * Down
     * Left
   * Each visited land cell is converted to `'0'` to mark it as visited.

4. **Avoid Recounting**

   * Since visited land is converted to water, it will not be counted again.

5. **Final Count**

   * The counter reflects the total number of distinct islands.

---

## Full Solution

```java
class Solution {

    // Depth-First Search to explore connected land cells
    public static void dfs(char[][] grid, int row, int col) {

        // Boundary check: return if indices are out of bounds
        if (row < 0 || col < 0 || row >= grid.length || col >= grid[0].length)
            return;

        // Process only land cells
        if (grid[row][col] == '1') {

            // Mark the current land cell as visited by converting it to water
            grid[row][col] = '0';

            // Explore all four adjacent directions
            dfs(grid, row - 1, col); // up
            dfs(grid, row, col + 1); // right
            dfs(grid, row + 1, col); // down
            dfs(grid, row, col - 1); // left
        }
    }

    // Main function to count number of islands
    public int numIslands(char[][] grid) {
        int count = 0;

        // Traverse each cell in the grid
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {

                // If an unvisited land cell is found
                if (grid[i][j] == '1') {

                    // Explore the entire island
                    dfs(grid, i, j);

                    // Increment island count
                    count++;
                }
            }
        }

        return count;
    }
}
```

---

## Key Insights

* This is a **connected components** problem on a grid.
* DFS ensures all adjacent land is explored in one traversal.
* Modifying the grid in-place avoids extra memory for a visited array.
* The solution is optimal and widely accepted for this problem.

---

## Common Mistakes to Avoid

1. Forgetting boundary checks in DFS
2. Not marking visited cells
3. Counting the same island multiple times
4. Confusing diagonal connections (not allowed)
5. Using DFS without handling recursion depth limits

---

## Interview Relevance

This problem tests:

* Graph traversal fundamentals
* Recursive DFS logic
* Grid-based problem-solving
* Time and space complexity reasoning

It is a **classic LeetCode problem** frequently asked in technical interviews.