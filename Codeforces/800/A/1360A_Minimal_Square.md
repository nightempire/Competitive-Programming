# A. Minimal Square

## Platform

Codeforces

## Problem Link

[A. Minimal Square](https://codeforces.com/problemset/problem/1360/A)

## Problem Statement

You are given multiple test cases.
For each test case, two integers `a` and `b` are provided, representing the sides of a rectangle.

Your task is to determine the **minimum possible area of a square** such that the rectangle of size `a × b` can fit entirely inside the square.

The rectangle **cannot be rotated**, but you may choose the square size optimally.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains two integers `a` and `b`.

## Output Format

For each test case, print a single integer — the **area of the minimal square** that can contain the rectangle.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ a, b ≤ 10^9`

## Examples

### Example 1

Input

```
3
2 3
4 4
1 5
```

Explanation

* Test case 1: Rectangle `2 × 3`
  Minimal square side = `max(3, 2×2) = 4` → area = `16`
* Test case 2: Rectangle `4 × 4`
  Already a square → area = `16`
* Test case 3: Rectangle `1 × 5`
  Minimal square side = `5` → area = `25`

Output

```
16
16
25
```

### Example 2

Input

```
1
6 2
```

Explanation

* Rectangle sides reordered as `2 × 6`
* `2 × 2 = 4 < 6`, so square side = `6`
* Area = `36`

Output

```
36
```

## Approach

Greedy comparison using maximum side constraints.

## Intuition

To fit a rectangle inside a square:

* The square side must be **at least as large as the longer side**
* Additionally, if the shorter side is doubled and exceeds the longer side, the square must expand accordingly

Thus, the minimal square side is:

```
max(b, 2 × a)   (after ensuring a ≤ b)
```

The required answer is simply the square of this value.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read integers `a` and `b`
  * Ensure `a ≤ b` by swapping if necessary
  * If `2 × a > b`, the square side becomes `2 × a`
  * Otherwise, the square side remains `b`
  * Print the square of the chosen side

## Visual Walkthrough

### Test Case 1

Input:

```
a = 2, b = 3
```

After ordering:

```
a = 2, b = 3
```

Check:

```
2 × 2 = 4 > 3
```

Square side:

```
4
```

Area:

```
16
```

---

### Test Case 2

Input:

```
a = 1, b = 5
```

Check:

```
2 × 1 = 2 < 5
```

Square side:

```
5
```

Area:

```
25
```

---

### Test Case 3

Input:

```
a = 4, b = 4
```

Already square:

```
side = 4
```

Area:

```
16
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case involves a constant number of arithmetic and comparison operations.

### Space Complexity

O(1)

Only a few integer variables are used.

## Solution Explanation

The solution ensures the rectangle always fits inside the smallest possible square by considering two constraints:

* The square must be large enough for the longer side
* The shorter side, when doubled, may force a larger square

By taking the maximum of these two values, the minimal square side is obtained efficiently.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while (t--) {

        // Dimensions of the rectangle
        int a, b;
        cin >> a >> b;

        // Ensure a <= b
        if (b < a) {
            int temp = a;
            a = b;
            b = temp;
        }

        // Determine minimal square area
        // If doubling the smaller side exceeds the larger side,
        // the square side must be doubled
        if (2 * a > b)
            cout << 4 * a * a << '\n';
        else
            cout << b * b << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| a | b | Output | Reason                |
| - | - | ------ | --------------------- |
| 2 | 3 | 16     | 2×2 > 3               |
| 4 | 4 | 16     | Already square        |
| 1 | 5 | 25     | Longer side dominates |
| 6 | 2 | 36     | Reordered, b²         |

## Edge Cases to Consider

* `a = b`
* One side equals `1`
* Very large input values

## Common Test Cases

* Rectangles with one side much larger
* Rectangles with equal sides
* Multiple test cases with mixed values

## Common Mistakes to Avoid

* Forgetting to reorder `a` and `b`
* Using `min(a, b)` incorrectly
* Miscalculating square area

## Interview Relevance

* Tests geometric reasoning
* Evaluates greedy decision-making
* Common math-based interview problem

## What This Problem Teaches

* Translating geometric constraints into arithmetic logic
* Importance of normalization (ordering values)
* Efficient use of comparisons

## Key Takeaways

* Always normalize inputs before applying logic
* Consider worst-case constraints explicitly
* Simple math can solve geometry problems effectively

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on logical reasoning and arithmetic correctness rather than complex algorithms.