# 1266. Minimum Time Visiting All Points

## Platform

LeetCode

## Problem Link

[https://leetcode.com/problems/minimum-time-visiting-all-points/](https://leetcode.com/problems/minimum-time-visiting-all-points/)

## Problem Statement

You are given an array `points`, where `points[i] = [xi, yi]` represents a point on a 2D plane.

You must visit all the points **in the given order**.
You start at the first point and move to the next one until all points are visited.

In one second, you can:

* Move vertically by 1 unit
* Move horizontally by 1 unit
* Move diagonally by 1 unit (both x and y change by 1)

Your task is to calculate the **minimum time in seconds** required to visit all the points.

## Input Format

* A 2D integer array `points`

  * `points[i][0]` represents the x-coordinate
  * `points[i][1]` represents the y-coordinate

## Output Format

Return a single integer representing the minimum time required to visit all points.

## Constraints

* `1 ≤ points.length ≤ 100`
* `points[i].length == 2`
* `-1000 ≤ xi, yi ≤ 1000`

## Examples

### Example 1

Input

```
points = [[1,1],[3,4],[-1,0]]
```

Explanation

Movement:

* From `(1,1)` to `(3,4)`

  * Horizontal distance = 2
  * Vertical distance = 3
  * Time required = `max(2,3) = 3`
* From `(3,4)` to `(-1,0)`

  * Horizontal distance = 4
  * Vertical distance = 4
  * Time required = `max(4,4) = 4`

Total time:

```
3 + 4 = 7
```

Output

```
7
```

### Example 2

Input

```
points = [[3,2],[-2,2]]
```

Explanation

* Horizontal distance = 5
* Vertical distance = 0
* Time required = `max(5,0) = 5`

Output

```
5
```

## Approach (Algorithm Type)

Greedy distance accumulation using Chebyshev distance.

## Intuition

Because diagonal movement is allowed, you can reduce both the x and y distance **simultaneously**.

The optimal strategy between two points is:

* Move diagonally as much as possible
* Then move straight for the remaining distance

This results in the minimum time being the **maximum of the horizontal and vertical distances** between two consecutive points.

## Algorithm Steps

* Initialize a variable `total` to store total time
* Iterate through the points from index `0` to `n-2`
* For each consecutive pair:

  * Compute absolute difference in x-coordinates
  * Compute absolute difference in y-coordinates
  * Add `max(dx, dy)` to `total`
* Return `total`

## Visual Walkthrough

Test Case 1:

```
(1,1) → (3,4)
dx = |3 - 1| = 2
dy = |4 - 1| = 3
time = 3
```

---

```
(3,4) → (-1,0)
dx = | -1 - 3 | = 4
dy = | 0 - 4 | = 4
time = 4
```

---

Total time:

```
3 + 4 = 7
```

## Complexity Analysis

### Time Complexity

O(n)
Each pair of consecutive points is processed once.

### Space Complexity

O(1)
Only constant extra space is used.

## Solution Explanation

The solution iterates through each consecutive pair of points and calculates the minimum time needed to move between them.

Since diagonal movement allows reducing both x and y coordinates in one second, the optimal time required is the **maximum** of the horizontal and vertical distances.

Summing this value for all consecutive pairs gives the final minimum time.

## Full Solution (Heavily Commented C++ Code)

```cpp
class Solution {
public:
    int minTimeToVisitAllPoints(vector<vector<int>>& points) {

        // Total number of points
        int n = points.size();

        // Variable to accumulate total time
        int total = 0;

        // Iterate through consecutive point pairs
        for (int i = 0; i < n - 1; i++) {

            // Calculate horizontal distance
            int dx = abs(points[i + 1][0] - points[i][0]);

            // Calculate vertical distance
            int dy = abs(points[i + 1][1] - points[i][1]);

            // Minimum time needed to move between two points
            // Diagonal movement allows reducing both distances simultaneously
            total += max(dx, dy);
        }

        // Return the total minimum time
        return total;
    }
};
```

## Test Cases Analysis

| Points               | dx, dy per move | Total Time |
| -------------------- | --------------- | ---------- |
| [[1,1],[3,4],[-1,0]] | (2,3), (4,4)    | 7          |
| [[3,2],[-2,2]]       | (5,0)           | 5          |
| [[0,0],[0,0]]        | (0,0)           | 0          |
| [[1,2],[3,2],[3,5]]  | (2,0), (0,3)    | 5          |

## Edge Cases to Consider

* Only one point
* Points with same x or y coordinate
* Negative coordinates
* Consecutive identical points

## Common Test Cases

* Straight horizontal movement
* Straight vertical movement
* Pure diagonal movement
* Mixed directional movement

## Common Mistakes to Avoid

* Using Manhattan distance instead of maximum distance
* Forgetting diagonal movement capability
* Incorrect absolute difference calculation

## Interview Relevance

* Tests understanding of movement optimization
* Demonstrates greedy distance calculation
* Common geometry-based interview problem

## What This Problem Teaches

* How movement rules affect distance metrics
* Applying Chebyshev distance in practice
* Simplifying problems using constraints

## Key Takeaways

* Diagonal moves minimize time
* Maximum of dx and dy determines optimal cost
* Simple iteration yields optimal performance

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on understanding movement constraints rather than complex algorithms and is frequently used to assess basic greedy reasoning.