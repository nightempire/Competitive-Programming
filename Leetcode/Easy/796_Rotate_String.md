## 796. Rotate String

## Platform

LeetCode

## Problem Link

[Rotate String](https://leetcode.com/problems/rotate-string/)

## Problem Statement

Given two strings `s` and `goal`, return `true` if and only if `s` can become `goal` after some number of **rotations**.

A rotation is defined as moving the leftmost character of the string to the rightmost position.

## Input Format

* Two strings `s` and `goal`

## Output Format

* Return `true` or `false`

## Constraints

* `1 ≤ s.length, goal.length ≤ 100`
* `s` and `goal` consist of lowercase English letters

## Examples

### Example 1

Input

```id="5xq8u1"
s = "abcde", goal = "cdeab"
```

Explanation

```id="q7b7uk"
abcde → bcdea → cdeab  (rotation achieved)
```

Output

```id="i0l7gq"
true
```

---

### Example 2

Input

```id="u8q9av"
s = "abcde", goal = "abced"
```

Explanation

```id="x8l6yy"
No sequence of rotations produces "abced"
```

Output

```id="n9uk4z"
false
```

---

### Example 3

Input

```id="b6z2cf"
s = "aaaa", goal = "aaaa"
```

Explanation

```id="n9p6qv"
Already equal → valid rotation
```

Output

```id="3fxk6p"
true
```

## Approach

String Matching (Concatenation + Substring Search)

## Intuition

If `goal` is a rotation of `s`, then:

```text
goal must be a substring of (s + s)
```

Why?

* Concatenating `s` with itself contains all possible rotations of `s`
* Example:

```text id="y1o9pl"
s = "abcde"
s+s = "abcdeabcde"
```

All rotations:

```text id="m3c7t1"
bcdea, cdeab, deabc, eabcd → all appear inside s+s
```

Thus, we just need to check if `goal` exists in `s + s`.

## Algorithm Steps

* If lengths of `s` and `goal` are not equal → return `false`
* Concatenate `s = s + s`
* For each index `i` in concatenated string:

  * Check if substring starting at `i` matches `goal`
* If any match is found → return `true`
* Else → return `false`

## Visual Walkthrough

### Case 1

```id="9ljhgj"
s = "abcde", goal = "cdeab"
```

```id="qyrxyo"
s+s = "abcdeabcde"

Check:
index 2 → "cdeab" → match → TRUE
```

---

### Case 2

```id="g0a0wz"
s = "abcde", goal = "abced"
```

```id="a7g7k2"
No substring match in "abcdeabcde"
```

---

### Case 3

```id="ijh2sl"
s = "aaaa", goal = "aaaa"
```

```id="5kmw9r"
Every rotation is identical → TRUE
```

## Complexity Analysis

### Time Complexity

**O(n²)**

* Outer loop runs `2n` times
* Inner comparison runs up to `n`

### Space Complexity

**O(n)**

* Concatenated string uses extra space

## Solution Explanation

The solution doubles the string `s` to capture all rotations implicitly. It then checks whether `goal` appears as a substring. Instead of using built-in substring search, it performs a manual comparison for each possible starting index.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

class Solution {
public:
    bool rotateString(string s, string goal) {

        // If lengths differ, rotation is impossible
        if(s.size() != goal.size()) return false;

        // Concatenate string with itself
        s += s;

        // Length of original string
        int n = goal.size();

        // Try every possible starting position
        for(int i = 0; i < n + n; i++) {

            int j = 0;

            // Compare substring with goal
            while(j < n && s[i + j] == goal[j]) {
                j++;
            }

            // If full match found
            if(j == n) return true;
        }

        // No match found
        return false;
    }
};
```

## Test Cases Analysis

| s     | goal  | s+s        | Match Exists | Output |
| ----- | ----- | ---------- | ------------ | ------ |
| abcde | cdeab | abcdeabcde | Yes          | true   |
| abcde | abced | abcdeabcde | No           | false  |
| aaaa  | aaaa  | aaaaaaaa   | Yes          | true   |
| ab    | ba    | abab       | Yes          | true   |

## Edge Cases to Consider

* Strings of length 1
* All characters identical
* Completely different strings
* Large strings with repeated patterns

## Common Test Cases

* Valid rotation cases
* Invalid rotation cases
* Same strings
* Reverse strings

## Common Mistakes to Avoid

* Forgetting to check equal lengths
* Not considering concatenation trick
* Incorrect substring matching bounds

## Interview Relevance

* Classic string manipulation problem
* Tests understanding of rotations
* Introduces substring search techniques

## What This Problem Teaches

* Using string concatenation for rotation problems
* Efficient substring search ideas
* Avoiding brute-force rotation simulation

## Key Takeaways

* Rotation problems often reduce to substring checks
* `s + s` is a powerful trick
* Always verify constraints before processing

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The key insight is recognizing that all rotations are contained within the doubled string, after which implementation becomes straightforward.