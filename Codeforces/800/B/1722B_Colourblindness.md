# B. Colourblindness

## Platform

Codeforces

## Problem Link

[B. Colourblindness](https://codeforces.com/problemset/problem/1722/B)

## Problem Statement

You are given two strings of equal length representing two rows of colors.

Each character in the strings is one of the following:

* `'R'` — Red
* `'G'` — Green
* `'B'` — Blue

A colourblind person **cannot distinguish between Green (`G`) and Blue (`B`)**, but **can distinguish Red (`R`) from both**.

Determine whether the two rows appear **identical to a colourblind person**.

For each test case, output `"YES"` if they look the same, otherwise output `"NO"`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * A single integer `n`, the length of the strings.
  * A string `r1` of length `n`.
  * A string `r2` of length `n`.

## Output Format

For each test case, print `"YES"` if the two strings are identical for a colourblind person, otherwise print `"NO"`.

## Constraints

* `1 ≤ t ≤ 10⁴`
* `1 ≤ n ≤ 100`
* `r1[i], r2[i] ∈ {R, G, B}`

## Examples

### Example 1

Input

```
1
3
RGB
RBG
```

Explanation

From a colourblind perspective:

* `G` and `B` are considered the same
* Both strings effectively become:

```
RXX
```

Output

```
YES
```

---

### Example 2

Input

```
1
3
RGB
GBR
```

Explanation

At index `0`:

* `r1[0] = R`
* `r2[0] = G`

Red is distinguishable, so the rows differ.

Output

```
NO
```

---

### Example 3

Input

```
1
4
GGGB
BBBB
```

Explanation

All characters are either `G` or `B`, which are indistinguishable.

Output

```
YES
```

## Approach

**Character-wise comparison with color equivalence**

## Intuition

Since a colourblind person cannot tell `G` and `B` apart:

* Any position containing only `G` or `B` in both strings is acceptable.
* A mismatch occurs **only if one position has `R` and the other has `G` or `B`**.

Thus, checking for mismatches involving `R` is sufficient.

## Algorithm Steps

* Read the number of test cases.
* For each test case:

  * Read `n`, `r1`, and `r2`.
  * Traverse each index:

    * If one character is `'R'` and the other is not `'R'`, mark mismatch.
  * If no mismatch is found, output `"YES"`, otherwise `"NO"`.

## Visual Walkthrough

### Case 1

```
r1: R G B
r2: R B G
```

Interpretation for colourblind person:

```
R X X
R X X
```

Result: **Same**

---

### Case 2

```
r1: R G B
r2: G B R
```

Mismatch at index `0`:

```
R ≠ X
```

Result: **Different**

---

### Case 3

```
r1: G G G B
r2: B B B B
```

All positions are `G/B` → indistinguishable

Result: **Same**

## Complexity Analysis

### Time Complexity

**O(n) per test case**

Each character is compared once.

### Space Complexity

**O(1)**

Only constant extra variables are used.

## Solution Explanation

The solution checks each position independently.
If a mismatch involving `'R'` is found, the strings are distinguishable to a colourblind person.

If no such mismatch exists, the strings are considered identical.

This direct comparison avoids unnecessary transformations and is optimal.

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

        // Length of the strings
        int n;
        cin >> n;

        // Two color strings
        string r1, r2;
        cin >> r1 >> r2;

        // Flag to detect invalid mismatch
        bool flag = false;

        // Compare each character
        for (int i = 0; i < n; i++) {

            // If one is 'R' and the other is not 'R'
            // then colorblind person can detect the difference
            if ((r1[i] == 'R' || r2[i] == 'R') && r1[i] != r2[i]) {
                flag = true;
                break;
            }
        }

        // Output result
        cout << (flag ? "NO\n" : "YES\n");
    }

    return 0;
}
```

## Test Cases Analysis

| r1  | r2  | Result | Reason                 |
| --- | --- | ------ | ---------------------- |
| RGB | RBG | YES    | G and B are equivalent |
| RGB | GBR | NO     | R mismatch             |
| GGG | BBB | YES    | All indistinguishable  |
| RRR | RRR | YES    | Exact match            |

## Edge Cases to Consider

* All characters are `R`
* Strings contain only `G` and `B`
* Single-character strings
* Early mismatch involving `R`

## Common Test Cases

* Mixed `R`, `G`, `B` strings
* Completely identical strings
* Completely different but colourblind-equivalent strings

## Common Mistakes to Avoid

* Treating `G` and `B` as different
* Comparing characters directly without equivalence logic
* Forgetting early termination on mismatch

## Interview Relevance

* Tests string comparison logic
* Evaluates conditional reasoning
* Simple but detail-oriented problem

## What This Problem Teaches

* Handling equivalence classes
* Simplifying comparisons with logical conditions
* Careful interpretation of problem constraints

## Key Takeaways

* Not all characters need exact equality
* Identify and isolate the distinguishing cases
* Early exits improve efficiency

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on logical comparison rather than algorithms, making it ideal for beginners and quick interview warm-up questions.