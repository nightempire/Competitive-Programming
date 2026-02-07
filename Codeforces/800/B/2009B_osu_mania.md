# B_osu_mania

## Platform

Codeforces

## Problem Link

[B. Osu!mania](https://codeforces.com/problemset/problem/2009/B)

## Problem Statement

You are given the layout of notes in the rhythm game **Osu!mania**.

For each test case, there are `n` rows representing beats.
Each row contains exactly **one `'#'` character** and three `'.'` characters, representing which of the **four columns** the note appears in.

The rows are given **from top to bottom**, but the notes must be processed **from bottom to top**.

Your task is to determine, for each row, **which column (1 to 4)** contains the `'#'`, and output the result in the required order.

## Input Format

* The first line contains an integer `t`, the number of test cases
* For each test case:

  * An integer `n`, the number of rows
  * `n` lines follow, each a string of length `4` consisting of `'.'` and `'#'`

## Output Format

* For each test case, print `n` integers
* Each integer represents the column index (1-based) where `'#'` appears
* Values must be printed **from bottom row to top row**

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n ≤ 100`
* Each row contains exactly one `'#'`
* Each string has length `4`

## Examples

### Example 1

Input

```
1
3
.#..
..#.
#...
```

Explanation

Rows are read top to bottom but processed bottom to top:

```
Row 3: #... → column 1
Row 2: ..#. → column 3
Row 1: .#.. → column 2
```

Output

```
1 3 2
```

---

### Example 2

Input

```
1
1
...#
```

Explanation

Only one row exists.
The `'#'` is in column 4.

Output

```
4
```

## Approach

**Reverse Row Processing with Direct Character Scan**

## Intuition

Each row has exactly one note (`'#'`), and the column position is independent of other rows.

However, the key observation is:

* Input is given **top to bottom**
* Output is required **bottom to top**

So, results must be stored in reverse order while reading input.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read integer `n`
  * Create an array `res` of size `n`
  * For each row:

    * Read the string
    * Scan from left to right to find `'#'`
    * Store `(index + 1)` in `res[n - 1 - current_row]`
  * Print all values of `res` in order

## Visual Walkthrough

### Case 1

Input rows (top → bottom):

```
.#..
..#.
#...
```

Processing order (bottom → top):

```
#...  → 1
..#.  → 3
.#..  → 2
```

Final output:

```
1 3 2
```

---

### Case 2

Input:

```
...#
```

Only one row:

```
Column = 4
```

Output:

```
4
```

## Complexity Analysis

### Time Complexity

**O(n)**

Each row is scanned once, and each scan checks exactly 4 characters.

### Space Complexity

**O(n)**

An array of size `n` is used to store the results.

## Solution Explanation

The solution reads each row and immediately determines the column of the `'#'`.

Because the required output order is reversed, the result is stored using a decreasing index.

This avoids extra reversing steps and keeps the logic simple and efficient.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int n;
        cin >> n;

        // Array to store results in reverse order
        int res[n];

        // Read rows from top to bottom
        while (n--) {

            string s;
            cin >> s;

            // Find the position of '#'
            for (int i = 0; i < 4; i++) {
                if (s[i] == '#') {
                    // Store column index (1-based) in reverse order
                    res[n] = i + 1;
                    break;
                }
            }
        }

        // Output the result
        for (int x : res) {
            cout << x << " ";
        }
        cout << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Rows (`n`) | Input Pattern | Output                |
| ---------- | ------------- | --------------------- |
| 1          | `...#`        | 4                     |
| 3          | Mixed rows    | Valid column indices  |
| 100        | Random        | Correct reverse order |

## Edge Cases to Consider

* Minimum size (`n = 1`)
* `'#'` at first column
* `'#'` at last column
* Multiple test cases

## Common Test Cases

* Single-row input
* Alternating column positions
* All rows having `'#'` in same column

## Common Mistakes to Avoid

* Printing in input order instead of reverse
* Using 0-based index in output
* Forgetting that each row has exactly one `'#'`

## Interview Relevance

* Tests array indexing and order handling
* Evaluates careful input/output processing
* Common pattern-reversal problem

## What This Problem Teaches

* Handling reversed output requirements
* Efficient scanning of fixed-size strings
* Attention to problem statement details

## Key Takeaways

* Input order and output order may differ
* Reverse storage avoids extra processing
* Simple scans are optimal for fixed-size data

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The logic is straightforward, but careful handling of order reversal is essential to avoid wrong answers.