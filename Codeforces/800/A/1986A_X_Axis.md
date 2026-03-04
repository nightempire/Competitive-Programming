# A_X_Axis

## Platform

Codeforces

## Problem Link

[A. X-Axis](https://codeforces.com/problemset/problem/1986/A)

## Problem Statement

Three points are located on the **X-axis** at integer coordinates.
You are given their positions.

Your task is to determine the **minimum total distance** required to move all three points to a **single meeting point on the X-axis**.

The meeting point can be **any integer coordinate**.

For each test case, compute the **minimum possible sum of distances** between the meeting point and the three given coordinates.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * A single line contains three integers representing the coordinates of the three points.

## Output Format

For each test case, print a single integer — the **minimum total distance** required.

## Constraints

* `1 ≤ t ≤ 1000`
* `0 ≤ xi ≤ 10`

## Examples

### Example 1

Input

```
3
1 2 3
2 2 2
1 1 10
```

Explanation

Test Case 1
Points: `1, 2, 3`

Optimal meeting point = `2`

Distances:

```
|1-2| = 1
|2-2| = 0
|3-2| = 1
```

Total distance:

```
1 + 0 + 1 = 2
```

Output

```
2
```

---

### Example 2

Input

```
1
5 7 9
```

Explanation

Sorted points:

```
5 7 9
```

Optimal meeting point = `7`

Distances:

```
|5-7| = 2
|7-7| = 0
|9-7| = 2
```

Total distance:

```
4
```

Output

```
4
```

---

### Example 3

Input

```
1
3 8 4
```

Explanation

Sorted points:

```
3 4 8
```

Optimal meeting point = `4`

Distances:

```
|3-4| = 1
|4-4| = 0
|8-4| = 4
```

Total distance:

```
5
```

Output

```
5
```

## Approach

Sorting with Median-Based Distance Minimization

## Intuition

For minimizing the sum of absolute distances on a number line, the **optimal meeting point is the median** of the values.

For three numbers:

```
a ≤ b ≤ c
```

The median is `b`.

Total minimum distance:

```
|a - b| + |b - b| + |c - b|
```

Which simplifies to:

```
(c - a)
```

Thus, instead of computing distances explicitly, we can:

* Sort the three numbers
* Subtract the smallest from the largest

This directly gives the minimum total movement required.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read three integers into an array.
  * Sort the array.
  * Compute the result as:

```
largest − smallest
```

* Print the result.

## Visual Walkthrough

### Test Case 1

Input

```
1 2 3
```

Sorted:

```
1 2 3
```

Meeting point:

```
2
```

Distances:

| Point | Distance |
| ----- | -------- |
| 1     | 1        |
| 2     | 0        |
| 3     | 1        |

Total distance:

```
2
```

---

### Test Case 2

Input

```
3 8 4
```

Sorted:

```
3 4 8
```

Meeting point:

```
4
```

Distances:

| Point | Distance |
| ----- | -------- |
| 3     | 1        |
| 4     | 0        |
| 8     | 4        |

Total distance:

```
5
```

---

### Test Case 3

Input

```
2 2 2
```

Sorted:

```
2 2 2
```

Meeting point:

```
2
```

Distances:

| Point | Distance |
| ----- | -------- |
| 2     | 0        |
| 2     | 0        |
| 2     | 0        |

Total distance:

```
0
```

## Complexity Analysis

### Time Complexity

O(1)

Each test case sorts only **three elements**, which is constant time.

### Space Complexity

O(1)

Only a fixed-size array of three integers is used.

## Solution Explanation

The program reads three coordinates for each test case.

Since the optimal meeting point for minimizing absolute distances is the **median**, sorting the three values allows easy identification of the smallest and largest numbers.

The minimal total distance equals the difference between the maximum and minimum coordinates.

This approach is efficient and avoids unnecessary distance calculations.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

int main() {

    // Variable to store number of test cases
    int t;

    // Read number of test cases
    cin >> t;

    // Process each test case
    while (t--) {

        // Array to store the three coordinates on the X-axis
        int nums[3];

        // Read the three coordinates
        cin >> nums[0] >> nums[1] >> nums[2];

        // Sort the coordinates in ascending order
        // After sorting:
        // nums[0] = smallest
        // nums[1] = median
        // nums[2] = largest
        sort(nums, nums + 3);

        // The minimal total distance equals (largest - smallest)
        // because the optimal meeting point is the median
        cout << nums[2] - nums[0] << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Points | Sorted Points | Minimum Distance |
| ------ | ------------- | ---------------- |
| 1 2 3  | 1 2 3         | 2                |
| 5 7 9  | 5 7 9         | 4                |
| 3 8 4  | 3 4 8         | 5                |
| 2 2 2  | 2 2 2         | 0                |

## Edge Cases to Consider

* All three coordinates are the same
* Two coordinates are identical
* Minimum coordinate values
* Maximum coordinate values

## Common Test Cases

* `1 2 3`
* `5 5 5`
* `10 0 5`
* `2 9 4`

## Common Mistakes to Avoid

* Forgetting to sort before computing the result
* Calculating distance from an incorrect meeting point
* Attempting brute-force search for the meeting point

## Interview Relevance

* Demonstrates understanding of median properties
* Introduces distance minimization on number lines
* Encourages mathematical optimization over brute force

## What This Problem Teaches

* Importance of the median in minimizing absolute distances
* Efficient handling of small fixed-size inputs
* Using sorting as a preprocessing step

## Key Takeaways

* The median minimizes total absolute distance
* Sorting helps identify smallest and largest elements quickly
* Mathematical insight simplifies implementation

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It primarily tests understanding of number line distance properties and basic sorting operations, making it suitable for beginners in competitive programming.