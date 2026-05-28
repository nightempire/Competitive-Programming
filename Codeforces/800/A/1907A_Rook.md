## 1907A. Rook

## Platform

Codeforces

## Problem Link

[Rook](https://codeforces.com/problemset/problem/1907/A)

## Problem Statement

You are given the position of a rook on a standard `8 × 8` chessboard.

The rook can move:

* Horizontally across the same row
* Vertically across the same column

Your task is to print all possible cells the rook can move to in one move, excluding its current position.

The board coordinates are represented as:

```text id="u8v3hy"
Columns: a to h
Rows:    1 to 8
```

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains a string `s` representing the rook’s position.

## Output Format

For each test case, print all cells the rook can move to, one per line.

## Constraints

* `1 ≤ t ≤ 64`
* `s` is a valid chessboard coordinate
* `s[0] ∈ {'a'...'h'}`
* `s[1] ∈ {'1'...'8'}`

## Examples

### Example 1

Input

```id="v9x2tz"
1
d5
```

Explanation

The rook at `d5` can move:

* Along row `5`
* Along column `d`

excluding `d5` itself.

Output

```id="z6t5pc"
a5
b5
c5
e5
f5
g5
h5
d1
d2
d3
d4
d6
d7
d8
```

---

### Example 2

Input

```id="g4n8kb"
1
a1
```

Explanation

The rook can move to all cells in:

* Row `1`
* Column `a`

except `a1`.

Output

```id="d8w0mf"
b1
c1
d1
e1
f1
g1
h1
a2
a3
a4
a5
a6
a7
a8
```

---

### Example 3

Input

```id="x2m9qe"
1
h8
```

Explanation

The rook moves along:

* Row `8`
* Column `h`

excluding `h8`.

Output

```id="t7f4zk"
a8
b8
c8
d8
e8
f8
g8
h1
h2
h3
h4
h5
h6
h7
```

## Approach

Simulation / Chessboard Traversal

## Intuition

A rook attacks:

* Every square in the same row
* Every square in the same column

So for a given position:

```text id="r7u4zx"
(column, row)
```

we generate:

* All columns with same row
* All rows with same column

while skipping the current square.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read rook position `s`
  * Traverse columns `a → h`

    * If column is not current column:

      * Print `(column + current row)`
  * Traverse rows `1 → 8`

    * If row is not current row:

      * Print `(current column + row)`

## Visual Walkthrough

### Case 1

```id="n3w9qb"
Position = d5
```

Horizontal moves:

```id="x6q2pe"
a5 b5 c5 e5 f5 g5 h5
```

Vertical moves:

```id="k4j8uy"
d1 d2 d3 d4 d6 d7 d8
```

---

### Case 2

```id="u5p7hr"
Position = a1
```

Horizontal:

```id="m8c2to"
b1 c1 d1 e1 f1 g1 h1
```

Vertical:

```id="q1y6ld"
a2 a3 a4 a5 a6 a7 a8
```

---

### Case 3

```id="w7e4vn"
Position = h8
```

Horizontal:

```id="a2r9ku"
a8 b8 c8 d8 e8 f8 g8
```

Vertical:

```id="f0x3lh"
h1 h2 h3 h4 h5 h6 h7
```

## Complexity Analysis

### Time Complexity

**O(1)**

The chessboard size is fixed (`8 × 8`), so exactly 14 moves are generated.

### Space Complexity

**O(1)**

No extra dynamic memory is used.

## Solution Explanation

The solution directly simulates rook movement:

* First generates all valid horizontal moves
* Then generates all valid vertical moves

The current square is skipped during both traversals.

## Full Solution

### C++ Implementation

```cpp id="e5t7qv"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Current rook position
        string s;
        cin >> s;

        // Traverse all columns and rows
        for(int i = 0; i < 8; i++) {

            // Horizontal movement
            // Skip current column
            if(s[0] - 'a' != i) {

                // Print new column with same row
                cout << (char)(i + 'a') << s[1] << '\n';
            }

            // Vertical movement
            // Skip current row
            if(s[1] - '1' != i) {

                // Print same column with new row
                cout << s[0] << i + 1 << '\n';
            }
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Position | Horizontal Moves | Vertical Moves | Total |
| -------- | ---------------- | -------------- | ----- |
| d5       | 7                | 7              | 14    |
| a1       | 7                | 7              | 14    |
| h8       | 7                | 7              | 14    |

## Edge Cases to Consider

* Corner positions (`a1`, `a8`, `h1`, `h8`)
* Middle board positions
* Edge rows or columns

## Common Test Cases

* `d4`
* `a1`
* `h8`
* `c7`

## Common Mistakes to Avoid

* Printing the original position
* Incorrect ASCII conversions
* Mixing row and column coordinates

## Interview Relevance

* Tests simulation skills
* Demonstrates coordinate manipulation
* Common beginner chessboard problem

## What This Problem Teaches

* Grid traversal techniques
* Character and integer conversions
* Chessboard coordinate handling

## Key Takeaways

* Rooks move independently in rows and columns
* ASCII arithmetic simplifies coordinate generation
* Simulation problems often require careful boundary handling

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The problem focuses on simple simulation and coordinate generation without requiring advanced algorithms.