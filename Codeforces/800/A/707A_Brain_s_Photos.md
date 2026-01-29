# A. Brain's Photos

## Platform

Codeforces

## Problem Link

[A. Brain's Photos](https://codeforces.com/problemset/problem/707/A)

## Problem Statement

You are given a photograph represented as a grid of pixels with `m` rows and `n` columns.

Each pixel is represented by a character indicating its color:

* `'B'` — Black
* `'W'` — White
* `'G'` — Gray
* `'C'` — Cyan
* `'M'` — Magenta
* `'Y'` — Yellow

The photo is considered **black and white** if **all pixels are only `'B'`, `'W'`, or `'G'`**.
If **any pixel** has a color other than these three, the photo is considered **colored**.

Determine whether the photo is black and white or colored.

## Input Format

* Two integers `m` and `n` — number of rows and columns.
* `m` lines follow, each containing `n` characters representing the pixels.

## Output Format

* Print `#Black&White` if the photo is black and white.
* Print `#Color` if the photo is colored.

## Constraints

* `1 ≤ m, n ≤ 100`
* Each pixel is one of `{B, W, G, C, M, Y}`

## Examples

### Example 1

Input

```
2 3
B W B
W G B
```

Explanation

All pixels are among `{B, W, G}`, so the image is black and white.

Output

```
#Black&White
```

---

### Example 2

Input

```
2 2
B C
W G
```

Explanation

The pixel `'C'` (Cyan) is a colored pixel.

Output

```
#Color
```

---

### Example 3

Input

```
1 1
Y
```

Explanation

`'Y'` (Yellow) is a colored pixel.

Output

```
#Color
```

## Approach

**Grid traversal with color validation**

## Intuition

The decision depends on whether **any pixel** falls outside the allowed black-and-white set `{B, W, G}`.

* If even one pixel is colored (`C`, `M`, or `Y`), the entire photo is colored.
* Otherwise, it is black and white.

Thus, a simple scan of all pixels is sufficient.

## Algorithm Steps

* Read integers `m` and `n`.
* Initialize a flag to track the presence of colored pixels.
* Traverse the grid:

  * Read each pixel.
  * If the pixel is not `'B'`, `'W'`, or `'G'`, set the flag.
* After scanning all pixels:

  * If the flag is set, print `#Color`.
  * Otherwise, print `#Black&White`.

## Visual Walkthrough

### Case 1

```
B W B
W G B
```

All pixels ∈ `{B, W, G}`
→ **Black & White**

---

### Case 2

```
B C
W G
```

Pixel `'C'` detected
→ **Color**

---

### Case 3

```
Y
```

Pixel `'Y'` detected
→ **Color**

## Complexity Analysis

### Time Complexity

**O(m × n)**

Each pixel is examined exactly once.

### Space Complexity

**O(1)**

Only a single boolean flag is used.

## Solution Explanation

The solution performs a straightforward grid traversal.
It checks whether each pixel belongs to the allowed black-and-white color set.

The moment a colored pixel is found, the final answer is determined.
This ensures correctness with minimal computation.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of rows and columns
    int m, n;
    cin >> m >> n;

    // Flag to indicate presence of colored pixels
    bool flag = false;

    // Traverse the entire grid
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {

            char pixel;
            cin >> pixel;

            // If pixel is not black, white, or gray,
            // then the image is colored
            if (pixel != 'B' && pixel != 'W' && pixel != 'G') {
                flag = true;
            }
        }
    }

    // Output result based on the flag
    cout << (flag ? "#Color" : "#Black&White");

    return 0;
}
```

## Test Cases Analysis

| Grid Size | Pixels Present | Result       |
| --------- | -------------- | ------------ |
| 2 × 3     | B, W, G only   | #Black&White |
| 2 × 2     | Contains C     | #Color       |
| 1 × 1     | Y              | #Color       |
| 3 × 3     | All B          | #Black&White |

## Edge Cases to Consider

* Single pixel image
* All pixels black
* Exactly one colored pixel
* Maximum grid size

## Common Test Cases

* Mixed black-and-white grids
* Grids with one colored pixel
* Fully colored grids

## Common Mistakes to Avoid

* Forgetting that `G` is allowed
* Checking only part of the grid
* Printing incorrect output format

## Interview Relevance

* Tests grid traversal
* Evaluates conditional logic
* Simple input parsing and validation

## What This Problem Teaches

* Efficient grid scanning
* Early decision logic
* Careful interpretation of allowed values

## Key Takeaways

* One invalid element can change the entire result
* Simple loops often solve classification problems
* Always check constraints carefully

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It requires basic iteration and condition checking, making it ideal for beginners and quick screening questions.