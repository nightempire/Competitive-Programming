# B_Not_Quite_Latin_Square

## Platform

Codeforces

## Problem Link

[B. Not Quite Latin Square](https://codeforces.com/problemset/problem/1915/B)

## Problem Statement

You are given a 3 × 3 grid representing a Latin square that should contain exactly one occurrence of each of the characters:

```
A, B, C
```

in every row.

However, one cell in the grid contains a `'?'` instead of a letter.

Your task is to determine which letter (`A`, `B`, or `C`) should replace the `'?'` so that every row contains all three distinct letters.

---

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * Three lines follow.
  * Each line contains a string of length 3.
  * Each character is either `A`, `B`, `C`, or `?`.
  * Exactly one `'?'` appears in the grid.

---

## Output Format

For each test case, print the letter (`A`, `B`, or `C`) that replaces the `'?'`.

---

## Constraints

* `1 ≤ t ≤ 100`
* Each grid is 3 × 3
* Exactly one `'?'` exists per test case

---

## Examples

### Example 1

Input

```
1
ABC
A?C
ABC
```

Explanation

Second row is `A ? C`.

The missing letter in that row is `B`.

Output

```
B
```

---

### Example 2

Input

```
1
AB?
ABC
ABC
```

Explanation

First row is `A B ?`.

Missing letter is `C`.

Output

```
C
```

---

### Example 3

Input

```
1
ABC
ABC
A?C
```

Explanation

Third row is `A ? C`.

Missing letter is `B`.

Output

```
B
```

---

## Approach (Algorithm Type)

**Bitwise XOR Trick (Character Parity Technique)**

---

## Intuition

In each row, the characters must be:

```
A, B, C
```

If we compute:

```
A ^ B ^ C
```

and then XOR it with all characters in the grid (including the `'?'`), the final result will isolate the missing character.

Why this works:

* XOR of a character with itself cancels out.
* Since every valid letter appears exactly once in a row except the missing one,
* The remaining unmatched value after XOR operations will be the missing letter.

This eliminates the need for row-wise checking.

---

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Initialize:

    ```
    ans = 'A' ^ 'B' ^ 'C' ^ '?'
    ```
  * Read 3 strings.
  * For every character in the 3 × 3 grid:

    * XOR it with `ans`.
  * Print `ans`.

---

## Visual Walkthrough

### Test Case 1

Grid:

```
ABC
A?C
ABC
```

Initial:

```
ans = A ^ B ^ C ^ ?
```

Now XOR with all grid characters:

All matching letters cancel out due to XOR property.

Remaining value:

```
B
```

Output → **B**

---

### Test Case 2

Grid:

```
AB?
ABC
ABC
```

After applying XOR logic:

Remaining character → **C**

---

### Test Case 3

Grid:

```
ABC
ABC
A?C
```

Remaining character → **B**

---

## Why XOR Works

XOR properties:

* `x ^ x = 0`
* `x ^ 0 = x`
* XOR is associative and commutative

Since all letters except the missing one cancel out, the leftover value is the missing letter.

---

## Complexity Analysis

### Time Complexity

**O(1) per test case**

* Grid size is fixed (3 × 3).
* Always processes 9 characters.
* For `t` test cases → O(t).

---

### Space Complexity

**O(1)**

* Only a few variables are used.
* No additional data structures required.

---

## Solution Explanation

The solution initializes `ans` with:

```
'A' ^ 'B' ^ 'C' ^ '?'
```

Then XORs every character from the input grid.

Because:

* Each valid letter appears twice (once in initialization and once in grid)
* They cancel out
* Only the missing character remains

This provides an elegant and highly efficient solution.

---

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Store the 3 rows of the grid
        string s[3];

        // Initialize ans with XOR of required characters and '?'
        // This prepares the base for cancellation logic
        char ans = 'A' ^ 'B' ^ 'C' ^ '?';

        // Read the grid
        for(int i = 0; i < 3; i++) {

            cin >> s[i];

            // XOR each character with ans
            for(int j = 0; j < 3; j++) {
                ans ^= s[i][j];
            }
        }

        // Print the missing character
        cout << ans << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| Grid Configuration  | Missing Letter | Output  |
| ------------------- | -------------- | ------- |
| A?C in row          | B              | B       |
| AB? in row          | C              | C       |
| ?BC in row          | A              | A       |
| Missing in last row | Depends        | Correct |

---

## Edge Cases to Consider

* `'?'` appears in first row
* `'?'` appears in last row
* `'?'` at first position
* `'?'` at last position

---

## Common Test Cases

* Missing `A`
* Missing `B`
* Missing `C`
* Different row positions

---

## Common Mistakes to Avoid

* Overcomplicating with frequency arrays
* Forgetting that exactly one `'?'` exists
* Misunderstanding XOR cancellation

---

## Interview Relevance

* Demonstrates clever use of bitwise operations
* Shows understanding of XOR properties
* Encourages thinking beyond brute force

---

## What This Problem Teaches

* XOR cancellation technique
* Efficient constant-time solutions
* Leveraging problem constraints effectively

---

## Key Takeaways

* XOR is powerful for parity-based problems.
* Fixed-size inputs allow constant-time tricks.
* Always exploit problem guarantees (exactly one missing value).

---

## Problem Difficulty Analysis

This is an **Easy-level** Codeforces problem.

While the brute-force row check is simple, the XOR trick provides an elegant and optimized approach, making it insightful for beginners.