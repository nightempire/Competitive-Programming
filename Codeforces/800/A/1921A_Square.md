# A_Square

## Platform

Codeforces

## Problem Link

[A. Square](https://codeforces.com/problemset/problem/1921/A)

## Problem Statement

You are given the coordinates of four points in a 2D plane. These points form the vertices of a square whose sides are parallel to the coordinate axes.

Your task is to compute the **area of the square**.

---

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * Four lines follow.
  * Each line contains two integers `x` and `y` — coordinates of a vertex.

---

## Output Format

For each test case, print a single integer — the area of the square.

---

## Constraints

* `1 ≤ t ≤ 100`
* `-1000 ≤ x, y ≤ 1000`
* The given four points always form a valid square.
* The square’s sides are parallel to the axes.

---

## Examples

### Example 1

Input

```
1
1 1
1 3
3 1
3 3
```

Explanation

Points form a square:

* Vertical side length = |3 − 1| = 2
* Area = 2² = 4

Output

```
4
```

---

### Example 2

Input

```
1
-1 -1
-1 2
2 -1
2 2
```

Explanation

Side length = |2 − (-1)| = 3
Area = 3² = 9

Output

```
9
```

---

## Approach (Algorithm Type)

**Geometric Observation with Coordinate Comparison**

---

## Intuition

Since:

* The square’s sides are parallel to the axes,
* Two points will share the same `x` coordinate (vertical alignment),
* Two points will share the same `y` coordinate (horizontal alignment).

To compute the side length:

* Find two points with the same `x`.
* Compute the absolute difference of their `y` coordinates.

That difference is the side length.

Area is:

```
side × side
```

---

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read the first point.
  * Read the remaining three points.
  * Whenever another point has the same `x` as the first point:

    * Compute side = |difference in y|.
  * Print `side × side`.

---

## Visual Walkthrough

### Test Case 1

Points:

```
(1,1)
(1,3)
(3,1)
(3,3)
```

Vertical pair:

```
(1,1) and (1,3)
```

Side:

```
|3 - 1| = 2
```

Area:

```
2 × 2 = 4
```

---

### Test Case 2

Points:

```
(-1,-1)
(-1,2)
(2,-1)
(2,2)
```

Vertical pair:

```
(-1,-1) and (-1,2)
```

Side:

```
|2 - (-1)| = 3
```

Area:

```
3 × 3 = 9
```

---

### Test Case 3

Points:

```
(5,5)
(5,8)
(8,5)
(8,8)
```

Side:

```
|8 - 5| = 3
```

Area:

```
9
```

---

## Complexity Analysis

### Time Complexity

Each test case:

* Reads 4 points.
* Performs constant comparisons.

Overall:

```
O(t)
```

---

### Space Complexity

```
O(1)
```

Only a fixed-size array for 4 points is used.

---

## Solution Explanation

The solution:

* Stores coordinates of four vertices.
* Compares x-coordinates.
* When a vertical alignment is found, calculates side length using `abs`.
* Squares the side length to obtain area.

Since the square is guaranteed to be axis-aligned, this method always works.

---

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
#include<cmath>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Array to store 4 points (x, y)
        int sq[4][2];

        // Side length of square
        int side = 1;

        // Read first point
        cin >> sq[0][0] >> sq[0][1];

        // Read remaining three points
        for(int i = 1; i < 4; i++) {

            cin >> sq[i][0] >> sq[i][1];

            // If x-coordinate matches first point,
            // compute vertical side length
            if(sq[0][0] == sq[i][0]) {

                // Absolute difference of y-coordinates
                side = abs(sq[0][1] - sq[i][1]);
            }
        }

        // Area of square
        cout << side * side << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| Points Example | Side Length | Area |
| -------------- | ----------- | ---- |
| (1,1)-(1,3)    | 2           | 4    |
| (-1,-1)-(-1,2) | 3           | 9    |
| (5,5)-(5,8)    | 3           | 9    |

---

## Edge Cases to Consider

* Negative coordinates
* Points given in random order
* Minimum possible side length (1)
* Maximum coordinate values

---

## Common Test Cases

* Perfect small square
* Larger coordinate values
* Negative coordinate square
* Random order input

---

## Common Mistakes to Avoid

* Forgetting absolute value
* Assuming points are in sorted order
* Using diagonal distance instead of side length

---

## Interview Relevance

* Tests coordinate geometry fundamentals
* Requires understanding of axis-aligned shapes
* Reinforces absolute difference logic

---

## What This Problem Teaches

* Geometric reasoning using coordinates
* Identifying patterns in structured inputs
* Simple area computation

---

## Key Takeaways

* Axis-aligned squares simplify geometry problems.
* Absolute difference gives distance along one axis.
* Always rely on constraints to simplify logic.

---

## Problem Difficulty Analysis

This is an **Easy-level** problem on Codeforces.

It primarily tests geometric observation and correct use of coordinate comparisons, making it suitable for beginners and early contest practice.