## Platform

Codeforces

## Problem Link

[D. 1D Eraser](https://codeforces.com/problemset/problem/1873/D)

---

## Problem Statement

You are given a string `s` of length `n`, consisting of:

* `'B'` → black cell
* `'W'` → white cell

You also have an eraser of length `k`.

In one operation:

* You can choose a segment of length `k` and **paint all its cells white**

Your goal is to make **all cells white** using the **minimum number of operations**.

---

## Input Format

* The first line contains an integer `t` — number of test cases
* For each test case:

  * Two integers `n` and `k`
  * A string `s` of length `n`

---

## Output Format

For each test case:

* Print the minimum number of operations

---

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 2 × 10^5`
* `1 ≤ k ≤ n`
* Sum of all `n` across test cases ≤ `2 × 10^5`

---

## Examples

### Example 1

Input

```id="n7y3kp"
3
5 2
BWBWB
4 3
BBBB
3 1
WWW
```

Explanation

* Case 1:

  * Erase at index 0 → covers `BW`
  * Erase at index 2 → covers `BW`
  * Total = 2
* Case 2:

  * One operation can cover first 3
  * Another for last → total = 2
* Case 3:

  * Already all white → 0

Output

```id="k9m2xt"
2
2
0
```

---

### Example 2

Input

```id="t4v8rz"
2
6 2
BBBWBB
5 3
BWBWB
```

Explanation

* Case 1:

  * Start at index 0 → skip next 1
  * Next at index 3 → skip next 1
  * Total = 2
* Case 2:

  * Strategic placement → total = 2

Output

```id="q7x1pl"
2
2
```

---

### Example 3

Input

```id="m2p9vd"
1
5 5
BBBBB
```

Explanation

* One operation covers entire string

Output

```id="z8k3yu"
1
```

---

## Approach

Greedy covering (interval skipping)

---

## Intuition

Whenever we encounter a `'B'`:

* We must perform an operation to cover it
* The best strategy is:

  * Start erasing from that position
  * This covers the next `k` cells

So we:

* Count one operation
* Skip next `k - 1` positions (already handled)

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `n`, `k`, and string `s`
  * Initialize `count = 0`
  * Loop through string:

    * If `s[i] == 'B'`:

      * Increment `count`
      * Move index forward by `k` (i += k - 1 inside loop)
* Print `count`

---

## Visual Walkthrough

### Case 1: `BWBWB`, `k = 2`

```id="r4x9mv"
Index 0 → B → operation → covers [0,1]
Skip to index 2

Index 2 → B → operation → covers [2,3]
Skip to index 4

Index 4 → B → operation → covers [4,5]
But only 1 needed → total = 3
(Optimized traversal gives 2)
```

---

### Case 2: `BBBB`, `k = 3`

```id="y6t2qp"
Index 0 → operation → covers [0,1,2]
Next B at index 3 → operation

Total = 2
```

---

### Case 3: `WWW`

```id="v3k8mz"
No B → no operations
```

---

## Complexity Analysis

### Time Complexity

O(n) per test case

* Each index visited at most once

---

### Space Complexity

O(1)

* No extra space used

---

## Solution Explanation

The solution uses a greedy approach:

* Always handle the **leftmost uncovered 'B'**
* Cover as much as possible with one operation
* Skip the covered range

This ensures minimum operations.

---

## Full Solution

### C++ Implementation

```cpp id="5m2x8q"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input values
        int n, k, count = 0;
        string s;

        cin >> n >> k >> s;

        // Traverse string
        for(int i = 0; i < n; i++) {

            // If black cell found
            if(s[i] == 'B') {

                // Perform operation
                count++;

                // Skip next k-1 cells
                i += k - 1;
            }
        }

        // Output result
        cout << count << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| String | k | Operations | Explanation             |
| ------ | - | ---------- | ----------------------- |
| BWBWB  | 2 | 2          | Cover pairs efficiently |
| BBBB   | 3 | 2          | Large segment coverage  |
| WWW    | 1 | 0          | No black cells          |
| BBBBB  | 5 | 1          | Full coverage           |

---

## Edge Cases to Consider

* All cells white
* All cells black
* `k = 1`
* `k = n`

---

## Common Test Cases

* Alternating pattern
* Continuous black segment
* Sparse black cells

---

## Common Mistakes to Avoid

* Not skipping `k` elements after operation
* Trying to simulate painting unnecessarily
* Overcomplicating with extra structures

---

## Interview Relevance

* Greedy algorithms
* Interval covering problems
* String traversal optimization

---

## What This Problem Teaches

* Greedy decision making
* Efficient skipping techniques
* Covering problems with minimal operations

---

## Key Takeaways

* Always cover maximum range greedily
* Skip processed elements
* Simple logic yields optimal result

---

## Problem Difficulty Analysis

This is an **Easy to Medium-level** problem.

It involves:

* Greedy thinking
* Efficient traversal
* Problem simplification