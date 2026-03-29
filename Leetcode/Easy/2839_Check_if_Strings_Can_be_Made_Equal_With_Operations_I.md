## Platform

LeetCode

## Problem Link

[2839. Check if Strings Can be Made Equal With Operations I](https://leetcode.com/problems/check-if-strings-can-be-made-equal-with-operations-i)

---

## Problem Statement

You are given two strings `s1` and `s2`, both of length `4`.

You are allowed to perform the following operation any number of times:

* Swap characters at indices:

  * `(0, 2)`
  * `(1, 3)`

Your task is to determine whether it is possible to make `s1` equal to `s2` using these operations.

Return `true` if possible, otherwise return `false`.

---

## Input Format

* Two strings `s1` and `s2` of length `4`

---

## Output Format

* Return `true` or `false`

---

## Constraints

* `s1.length == s2.length == 4`
* Strings consist of lowercase English letters

---

## Examples

### Example 1

Input

```id="5q3qwn"
s1 = "abcd"
s2 = "cdab"
```

Explanation

* Swap indices `(0,2)` → `cbad`
* Swap indices `(1,3)` → `cdab`

Output

```id="ztf21q"
true
```

---

### Example 2

Input

```id="m4t7i5"
s1 = "abcd"
s2 = "dacb"
```

Explanation

* Cannot match using allowed swaps

Output

```id="4m4jrv"
false
```

---

### Example 3

Input

```id="vlyexb"
s1 = "abdc"
s2 = "acbd"
```

Explanation

* Rearrangement not achievable with given swaps

Output

```id="8h7nrt"
false
```

---

## Approach

Parity-based grouping (fixed swap groups)

---

## Intuition

The allowed swaps restrict movement:

* Characters at indices `{0, 2}` can only swap among themselves
* Characters at indices `{1, 3}` can only swap among themselves

So effectively:

* Even positions form one group
* Odd positions form another group

For strings to be equal:

* The multiset of characters in even indices must match
* The multiset of characters in odd indices must match

---

## Algorithm Steps

* Compare:

  * `s1[0]` must match either `s2[0]` or `s2[2]`
  * `s1[2]` must match either `s2[2]` or `s2[0]`
  * `s1[1]` must match either `s2[1]` or `s2[3]`
  * `s1[3]` must match either `s2[3]` or `s2[1]`
* If all conditions are satisfied → return `true`
* Otherwise → return `false`

---

## Visual Walkthrough

### Case 1

```id="7yhe8r"
s1 = abcd
Groups:
Even → a, c
Odd  → b, d

s2 = cdab
Even → c, a
Odd  → d, b

Both groups match → valid
```

---

### Case 2

```id="7x0b3h"
s1 = abcd
Even → a, c
Odd  → b, d

s2 = dacb
Even → d, c  (mismatch)
```

---

### Case 3

```id="c7b7pa"
s1 = abdc
Even → a, d
Odd  → b, c

s2 = acbd
Even → a, b (mismatch)
```

---

## Complexity Analysis

### Time Complexity

O(1)

* Fixed-length strings → constant comparisons

---

### Space Complexity

O(1)

* No extra memory used

---

## Solution Explanation

The solution directly checks if each character in `s1` can map to a valid position in `s2` within its allowed swap group.

Instead of performing swaps, it verifies **group membership equivalence**, ensuring both strings can be transformed into each other.

---

## Full Solution

### C++ Implementation

```cpp
#include <string>
using namespace std;

class Solution {
public:
    bool canBeEqual(string s1, string s2) {

        // Check for valid mapping in even index group (0,2)
        // and odd index group (1,3)

        return  (s1[0] == s2[0] || s1[0] == s2[2]) &&
                (s1[1] == s2[1] || s1[1] == s2[3]) &&
                (s1[2] == s2[2] || s1[2] == s2[0]) &&
                (s1[3] == s2[3] || s1[3] == s2[1]);
    }
};
```

---

## Test Cases Analysis

| s1   | s2   | Even Match | Odd Match | Result |
| ---- | ---- | ---------- | --------- | ------ |
| abcd | cdab | Yes        | Yes       | true   |
| abcd | dacb | No         | Yes       | false  |
| abdc | acbd | No         | No        | false  |

---

## Edge Cases to Consider

* Strings already equal
* Duplicate characters
* All characters same
* Minimal length (always 4)

---

## Common Test Cases

* `"abcd" → "cdab"` → true
* `"abcd" → "abcd"` → true
* `"abcd" → "dcba"` → false

---

## Common Mistakes to Avoid

* Treating all positions as freely swappable
* Ignoring index grouping constraints
* Overcomplicating with permutations

---

## Interview Relevance

* Tests grouping and constraints reasoning
* Highlights invariant properties
* Efficient problem simplification

---

## What This Problem Teaches

* Partitioning problems into independent groups
* Avoiding brute-force swaps
* Logical equivalence checking

---

## Key Takeaways

* Not all swaps are allowed → constraints matter
* Group-based reasoning simplifies problems
* Constant-time solutions are often possible

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Logical constraints
* String manipulation
* Efficient validation