# C_Word_on_the_Paper

## Platform

Codeforces

## Problem Link

[C. Word on the Paper](https://codeforces.com/problemset/problem/1850/A)

## Problem Statement

You are given multiple test cases.
In each test case, you are given an **8×8 grid** representing a piece of paper.

* Each cell of the grid contains either:

  * a lowercase English letter, or
  * a dot (`.`), representing an empty cell

Your task is to **read the word written on the paper** by:

* Traversing the grid row by row
* Collecting all characters that are **not dots**
* Concatenating them in the order they appear

For each test case, output the resulting word.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * 8 lines follow, each containing a string of length 8
  * Each string consists of lowercase English letters or `.`

## Output Format

For each test case, output a single string — the word formed by concatenating all non-dot characters.

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* Each test case contains exactly `8` rows
* Each row has exactly `8` characters
* Characters are lowercase English letters or `.`

## Examples

### Example 1

Input

```
1
........
....c...
....o...
....d...
....e...
....f...
....o...
....r...
```

Explanation

Reading row by row and ignoring dots:

```
c o d e f o r
```

Output

```
codefor
```

### Example 2

Input

```
1
a.......
.b......
..c.....
...d....
....e...
.....f..
......g.
.......h
```

Explanation

Collected characters in order:

```
a b c d e f g h
```

Output

```
abcdefgh
```

## Approach

**Grid traversal with character filtering**

## Intuition

The grid does not require any complex pattern detection.
The only rule is:

* Ignore dots
* Keep every visible letter in reading order

Since the grid size is fixed (8×8), a simple nested loop is sufficient.

## Algorithm Steps

* Read integer `t`
* For each test case:

  * Initialize an empty string `res`
  * Repeat 8 times:

    * Read a string representing one row
    * For each character in the row:

      * If the character is not `.`, append it to `res`
  * Output `res`

## Visual Walkthrough

### Test Case 1

Grid:

```
. . . . a . . .
. . . . b . . .
. . . . c . . .
. . . . d . . .
. . . . e . . .
. . . . f . . .
. . . . g . . .
. . . . h . . .
```

Collected characters:

```
a b c d e f g h
```

Output:

```
abcdefgh
```

---

### Test Case 2

Grid:

```
. . . . . . . .
. x . . . . . .
. . y . . . . .
. . . z . . . .
. . . . . . . .
. . . . . . . .
. . . . . . . .
. . . . . . . .
```

Collected characters:

```
x y z
```

Output:

```
xyz
```

---

### Test Case 3

Grid:

```
. . . . . . . .
. . . . . . . .
. . . . . . . .
. . . . . . . .
. . . . . . . .
. . . . . . . .
. . . . . . . .
. . . . . . . .
```

Collected characters:

```
(empty)
```

Output:

```
(empty line)
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case

Each test case processes exactly `64` characters (`8 × 8`), which is constant.

### Space Complexity

**O(1)**

The result string stores at most `64` characters.
No additional memory proportional to input size is used.

## Solution Explanation

The solution reads the grid row by row and checks each character.
Whenever a character is not a dot, it is appended to the result string.

This directly follows the problem statement and avoids unnecessary data structures or checks.

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

        // String to store the final word
        string res = "";

        // Read the 8x8 grid
        for (int i = 0; i < 8; i++) {

            string s;
            cin >> s;

            // Collect non-dot characters
            for (char ch : s) {
                if (ch != '.') {
                    res += ch;
                }
            }
        }

        // Output the extracted word
        cout << res << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Visible Letters Pattern | Output   |
| --------- | ----------------------- | -------- |
| 1         | Vertical word           | codefor  |
| 2         | Diagonal letters        | abcdefgh |
| 3         | Single column letters   | xyz      |
| 4         | All dots                | (empty)  |

## Edge Cases to Consider

* Grid with no letters
* Letters scattered across different rows
* All letters in a single row or column

## Common Test Cases

* Exactly one letter per row
* Multiple letters in the same row
* Mixed dots and characters

## Common Mistakes to Avoid

* Printing dots instead of skipping them
* Reading fewer or more than 8 rows
* Resetting the result string incorrectly between test cases

## Interview Relevance

* Tests grid traversal
* Evaluates careful input handling
* Reinforces filtering logic

## What This Problem Teaches

* Efficient traversal of fixed-size grids
* Filtering data based on simple conditions
* Translating problem statements directly into code

## Key Takeaways

* Fixed constraints allow simple solutions
* Clear traversal order avoids mistakes
* Ignoring irrelevant data simplifies logic

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on straightforward grid processing and clean implementation rather than algorithmic complexity.