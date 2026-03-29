## Platform

LeetCode

## Problem Link

[2840. Check if Strings Can be Made Equal With Operations II](https://leetcode.com/problems/check-if-strings-can-be-made-equal-with-operations-ii)

---

## Problem Statement

You are given two strings `s1` and `s2` of equal length `n`.

You can perform the following operation any number of times:

* Swap characters at indices:

  * `(i, i + 2)` for any valid `i`

Your task is to determine whether it is possible to make `s1` equal to `s2` using these operations.

Return `true` if possible, otherwise return `false`.

---

## Input Format

* Two strings `s1` and `s2`

---

## Output Format

* Return `true` or `false`

---

## Constraints

* `1 ≤ n ≤ 10^5`
* `s1.length == s2.length`
* Strings consist of lowercase English letters

---

## Examples

### Example 1

Input

```id="n9d3sh"
s1 = "abcdba"
s2 = "cabdab"
```

Explanation

* Even indices → `{a, c, b}`
* Odd indices → `{b, d, a}`
* Both groups match → transformation possible

Output

```id="8c2zgl"
true
```

---

### Example 2

Input

```id="5y7u9t"
s1 = "abe"
s2 = "bea"
```

Explanation

* Even indices mismatch → cannot transform

Output

```id="zpl3m1"
false
```

---

### Example 3

Input

```id="6v5n2q"
s1 = "abc"
s2 = "abc"
```

Explanation

* Already equal

Output

```id="1ytxgk"
true
```

---

## Approach

Frequency counting with parity grouping

---

## Intuition

Allowed operation:

```
Swap (i, i+2)
```

This means:

* Characters can only move within:

  * **Even indices (0,2,4,...)**
  * **Odd indices (1,3,5,...)**

Thus:

* Even positions form one independent group
* Odd positions form another independent group

For transformation to be possible:

* Frequency of characters in **even indices must match**
* Frequency of characters in **odd indices must match**

---

## Algorithm Steps

* Initialize two arrays:

  * `even[26]` → for even indices
  * `odd[26]` → for odd indices

* Traverse strings:

  * For each index `i`:

    * If `i` is even:

      * Increment `even[s1[i]]`
      * Decrement `even[s2[i]]`
    * Else:

      * Increment `odd[s1[i]]`
      * Decrement `odd[s2[i]]`

* After traversal:

  * If all values in both arrays are `0` → return `true`
  * Otherwise → return `false`

---

## Visual Walkthrough

### Case 1

```id="c4m78p"
s1 = abcdba
s2 = cabdab

Even indices:
s1 → a c b
s2 → c b a

Match ✔

Odd indices:
s1 → b d a
s2 → a d b

Match ✔
```

---

### Case 2

```id="h29r9m"
s1 = abe
s2 = bea

Even indices:
s1 → a e
s2 → b a → mismatch ✘
```

---

### Case 3

```id="3wrz06"
s1 = abc
s2 = abc

Even → match
Odd  → match
```

---

## Complexity Analysis

### Time Complexity

O(n)

* Single pass through strings

---

### Space Complexity

O(1)

* Fixed size arrays (26 characters)

---

## Solution Explanation

The solution leverages the invariant that swaps only affect positions within the same parity group.

Instead of simulating swaps, it compares **character frequency distributions** within even and odd indices separately.

If both distributions match, transformation is guaranteed.

---

## Full Solution

### C++ Implementation

```cpp id="6jv3y4"
#include <string>
using namespace std;

class Solution {
public:
    bool checkStrings(string s1, string s2) {

        // Length of strings
        int n = s1.length();

        // Frequency arrays for odd and even indices
        int odd[26] = {0}, even[26] = {0};

        // Boolean flag to track parity (false = even, true = odd)
        bool parity = false;

        // Traverse both strings
        for(int i = 0; i < n; i++) {

            if(parity) {
                // Odd index
                odd[s1[i] - 'a']++;
                odd[s2[i] - 'a']--;
            }
            else {
                // Even index
                even[s1[i] - 'a']++;
                even[s2[i] - 'a']--;
            }

            // Flip parity
            parity = !parity;
        }

        // Check if both frequency arrays are balanced
        for(int i = 0; i < 26; i++) {
            if(odd[i] != 0 || even[i] != 0) {
                return false;
            }
        }

        return true;
    }
};
```

---

## Test Cases Analysis

| s1     | s2     | Even Match | Odd Match | Result |
| ------ | ------ | ---------- | --------- | ------ |
| abcdba | cabdab | Yes        | Yes       | true   |
| abe    | bea    | No         | Yes       | false  |
| abc    | abc    | Yes        | Yes       | true   |

---

## Edge Cases to Consider

* Strings of length `1`
* Strings with all identical characters
* Large strings (`n = 10^5`)
* Completely mismatched parity groups

---

## Common Test Cases

* `"abcd" → "cdab"` → true
* `"abc" → "bca"` → false
* `"aaaa" → "aaaa"` → true

---

## Common Mistakes to Avoid

* Ignoring parity grouping
* Using sorting on entire string instead of groups
* Forgetting to decrement frequencies for `s2`

---

## Interview Relevance

* Frequency counting technique
* Invariant-based reasoning
* Avoiding brute-force swaps

---

## What This Problem Teaches

* Grouping based on constraints
* Efficient comparison using frequency arrays
* Thinking in terms of invariants

---

## Key Takeaways

* Swaps define independent index groups
* Compare distributions, not positions
* Frequency arrays provide optimal solution

---

## Problem Difficulty Analysis

This is a **Medium-level** problem.

It involves:

* String manipulation
* Greedy insight
* Frequency-based validation