# 1927A_Make_it_White

## Platform

Codeforces

## Problem Link

[A. Make it White](https://codeforces.com/problemset/problem/1927/A)

## Problem Statement

You are given a string `s` of length `n` consisting of characters:

```
'B' (Black)
'W' (White)
```

You want to repaint a **single continuous segment** of the string so that all characters in that segment become `'W'`.

Your task is to determine the **minimum length of the segment** that must be repainted so that the entire string becomes white.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * An integer `n`
  * A string `s` of length `n`

## Output Format

* For each test case, print a single integer — the minimum length of the segment to repaint.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 10^5`
* `s[i] ∈ {'B', 'W'}`
* The string contains at least one `'B'`

## Examples

### Example 1

Input

```
1
5
WBBBW
```

Explanation

First `'B'` at index `1`
Last `'B'` at index `3`

Segment length:

```
3 - 1 + 1 = 3
```

Output

```
3
```

---

### Example 2

Input

```
1
4
BBBB
```

Explanation

First `'B'` at index `0`
Last `'B'` at index `3`

Segment length:

```
3 - 0 + 1 = 4
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
6
WWBWWB
```

Explanation

First `'B'` at index `2`
Last `'B'` at index `5`

Segment length:

```
5 - 2 + 1 = 4
```

Output

```
4
```

## Approach

**First and Last Occurrence Identification**

## Intuition

To make the entire string white:

* All `'B'` characters must be repainted.
* Since only **one continuous segment** can be repainted,
  the chosen segment must cover:

  * The **first occurrence of `'B'`**
  * The **last occurrence of `'B'`**

Any smaller segment would leave some `'B'` unpainted.

Therefore, the answer is simply:

```
(last index of 'B') - (first index of 'B') + 1
```

## Algorithm Steps

* Read number of test cases `t`.
* For each test case:

  * Read `n` and string `s`.
  * Traverse from left to right to find first `'B'`.
  * Traverse from right to left to find last `'B'`.
  * Print `last - first + 1`.

## Visual Walkthrough

### Case 1: `"WBBBW"`

```
Indices: 0 1 2 3 4
         W B B B W

First B = 1
Last B  = 3
Segment length = 3
```

---

### Case 2: `"BWBWB"`

```
Indices: 0 1 2 3 4
         B W B W B

First B = 0
Last B  = 4
Segment length = 5
```

---

### Case 3: `"WWBWW"`

```
Indices: 0 1 2 3 4
         W W B W W

First B = 2
Last B  = 2
Segment length = 1
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

The string is scanned at most twice.

### Space Complexity

**O(1)**

Only a few integer variables are used.

## Solution Explanation

The solution identifies the leftmost and rightmost `'B'` characters.

Since repainting must cover all black cells in one continuous segment, the minimal segment is exactly the range between these two positions.

This direct observation eliminates the need for simulation or extra data structures.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int n, first = 0, last = 0;
        cin >> n;

        string s;
        cin >> s;

        // Find first occurrence of 'B'
        for (int i = 0; i < n; i++) {
            if (s[i] == 'B') {
                first = i;
                break;
            }
        }

        // Find last occurrence of 'B'
        for (int i = n - 1; i >= 0; i--) {
            if (s[i] == 'B') {
                last = i;
                break;
            }
        }

        // Output minimum segment length
        cout << last - first + 1 << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input String | First B | Last B | Output |
| ------------ | ------- | ------ | ------ |
| `WBBBW`      | 1       | 3      | 3      |
| `BBBB`       | 0       | 3      | 4      |
| `WWBWWB`     | 2       | 5      | 4      |
| `WWBWW`      | 2       | 2      | 1      |

## Edge Cases to Consider

* Only one `'B'` in the string
* `'B'` at the beginning and end
* Large input size
* Multiple test cases

## Common Test Cases

* Consecutive `'B'` characters
* Scattered `'B'` characters
* `'B'` only at edges

## Common Mistakes to Avoid

* Forgetting `+1` in length calculation
* Not handling single `'B'` case
* Incorrect index traversal

## Interview Relevance

* Tests understanding of substring coverage
* Reinforces boundary detection techniques
* Common pattern for range-based problems

## What This Problem Teaches

* Importance of identifying boundary elements
* Simple range calculations
* Efficient string traversal

## Key Takeaways

* Covering all target elements often requires boundary-based logic
* Two linear scans are sufficient
* Minimal repaint equals distance between extremes

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It requires basic string scanning and simple arithmetic, making it ideal for beginner-level competitive programming practice.