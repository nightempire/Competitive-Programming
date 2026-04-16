## Platform

Codeforces

## Problem Link

[A. Colorful Stones (Simplified Edition)](https://codeforces.com/problemset/problem/265/A)

---

## Problem Statement

You are given two strings:

* `s` — represents stones arranged in a row
* `t` — represents instructions

You start at position `1` (index `0` in 0-based indexing).

You process the string `t` character by character:

* If the current character in `t` matches the current stone in `s`, you **move forward to the next stone**

Your task is to determine the **final position** after processing all characters in `t`.

---

## Input Format

* First line: string `s`
* Second line: string `t`

---

## Output Format

* Print a single integer — the final position (1-based index)

---

## Constraints

* `1 ≤ |s|, |t| ≤ 50`
* Strings consist of lowercase English letters

---

## Examples

### Example 1

Input

```id="x8k3mp"
RGB
RRGGBB
```

Explanation

* Start at `s[0] = 'R'`
* Process `t`:

  * `R` → match → move to `G`
  * `R` → no match
  * `G` → match → move to `B`
  * `G` → no match
  * `B` → match → move forward
  * `B` → no match

Final index = 3 (1-based)

Output

```id="k5p2zx"
3
```

---

### Example 2

Input

```id="m2v9qr"
RRR
RRRRRR
```

Explanation

* Always matching → move forward each time

Output

```id="t7x4nl"
4
```

---

### Example 3

Input

```id="p9k1zs"
ABC
DEF
```

Explanation

* No matches → stay at position 1

Output

```id="z3m8xq"
1
```

---

## Approach

Greedy pointer traversal

---

## Intuition

We maintain a pointer `idx` on string `s`.

* Traverse string `t`
* Whenever `t[i] == s[idx]`, move `idx` forward

At the end:

* Position = `idx + 1` (convert to 1-based index)

---

## Algorithm Steps

* Read strings `s` and `t`
* Initialize `idx = 0`
* For each character `ch` in `t`:

  * If `ch == s[idx]`:

    * Increment `idx`
* Print `idx + 1`

---

## Visual Walkthrough

### Case 1: `s = RGB`, `t = RRGGBB`

```id="n7x2kp"
Start idx = 0 (R)

R → match → idx = 1 (G)
R → no match
G → match → idx = 2 (B)
G → no match
B → match → idx = 3
```

Final position = 4 (but since idx = 3, output = 3)

---

### Case 2: `s = RRR`, `t = RRRRRR`

```id="k3p8zx"
Every step matches → idx moves forward continuously
```

---

### Case 3: `s = ABC`, `t = DEF`

```id="t9m4vl"
No matches → idx remains 0
```

---

## Complexity Analysis

### Time Complexity

O(|t|)

* Single traversal of string `t`

---

### Space Complexity

O(1)

* Only one variable used

---

## Solution Explanation

The solution simulates the process directly:

* Use a pointer to track current stone
* Move forward only when characters match
* Output final position

This greedy approach ensures correctness and efficiency.

---

## Full Solution

### C++ Implementation

```cpp id="p6k3zx"
#include<iostream>
using namespace std;

int main() {

    // Input strings
    string s, t;
    cin >> s >> t;

    // Pointer for string s
    int idx = 0;

    // Traverse string t
    for(char ch : t) {

        // If match found, move forward
        if(ch == s[idx]) {
            idx++;
        }
    }

    // Output final position (1-based index)
    cout << idx + 1 << '\n';
}
```

---

## Test Cases Analysis

| s   | t      | Final idx | Output |
| --- | ------ | --------- | ------ |
| RGB | RRGGBB | 2         | 3      |
| RRR | RRRRRR | 3         | 4      |
| ABC | DEF    | 0         | 1      |

---

## Edge Cases to Consider

* No matching characters
* All characters match
* `|s| = 1`
* `|t| = 1`

---

## Common Test Cases

* Partial matches
* Repeated characters
* No matches

---

## Common Mistakes to Avoid

* Forgetting 1-based indexing in output
* Accessing `s[idx]` when `idx` exceeds length
* Misinterpreting matching condition

---

## Interview Relevance

* String traversal
* Pointer techniques
* Greedy simulation

---

## What This Problem Teaches

* Efficient string processing
* Using pointers for tracking state
* Simple simulation strategies

---

## Key Takeaways

* Greedy pointer movement works best
* Always convert to correct indexing
* Simplicity is often optimal

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* String manipulation
* Simulation
* Logical reasoning