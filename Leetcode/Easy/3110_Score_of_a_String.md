# 3110. Score of a String

## Platform

LeetCode

## Problem Link

[3110. Score of a String](https://leetcode.com/problems/score-of-a-string/)

## Problem Statement

You are given a string `s` consisting of lowercase English letters.

The **score of the string** is defined as the **sum of the absolute differences** between the ASCII values of **adjacent characters** in the string.

Your task is to compute and return the score of the given string.

## Input Format

* A single string `s`
* The string consists of lowercase English letters only

## Output Format

* Return an integer representing the score of the string

## Constraints

* `2 ≤ s.length ≤ 100`
* `s[i] ∈ {'a' ... 'z'}`

## Examples

### Example 1

Input

```
"hello"
```

Explanation

ASCII values:

```
'h' = 104
'e' = 101
'l' = 108
'l' = 108
'o' = 111
```

Differences:

```
|104 - 101| = 3
|101 - 108| = 7
|108 - 108| = 0
|108 - 111| = 3
```

Score:

```
3 + 7 + 0 + 3 = 13
```

Output

```
13
```

---

### Example 2

Input

```
"zaz"
```

Explanation

```
|122 - 97| = 25
|97 - 122| = 25
```

Score:

```
50
```

Output

```
50
```

---

### Example 3

Input

```
"aa"
```

Explanation

```
|97 - 97| = 0
```

Output

```
0
```

## Approach

**Linear Traversal with ASCII Difference Calculation**

## Intuition

The score depends **only on adjacent characters**.

For each adjacent pair:

* Convert characters to their ASCII values
* Compute the absolute difference
* Add it to the total score

Since each pair is independent, a single pass through the string is sufficient.

## Algorithm Steps

* Initialize `score = 0`
* Traverse the string from index `1` to `n - 1`
* For each index `i`:

  * Compute `abs(s[i] - s[i - 1])`
  * Add it to `score`
* Return `score`

## Visual Walkthrough

### Case 1: `"abc"`

```
'a' → 'b' : |97 - 98| = 1
'b' → 'c' : |98 - 99| = 1
Total Score = 2
```

---

### Case 2: `"az"`

```
'a' → 'z' : |97 - 122| = 25
Total Score = 25
```

---

### Case 3: `"mm"`

```
'm' → 'm' : |109 - 109| = 0
Total Score = 0
```

## Complexity Analysis

### Time Complexity

**O(n)**

The string is traversed once, where `n` is the length of the string.

### Space Complexity

**O(1)**

Only a constant amount of extra memory is used.

## Solution Explanation

The solution iterates through the string and computes the absolute difference between consecutive characters using their ASCII values.

This direct approach avoids unnecessary data structures and ensures optimal performance for the given constraints.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    int scoreOfString(string s) {

        // Length of the string
        int n = s.length();

        // Variable to store the total score
        int score = 0;

        // Traverse adjacent character pairs
        for (int i = 1; i < n; i++) {

            // Add absolute difference of ASCII values
            score += abs(s[i - 1] - s[i]);
        }

        // Return the final score
        return score;
    }
};
```

## Test Cases Analysis

| Input String | Adjacent Differences | Output |
| ------------ | -------------------- | ------ |
| `"aa"`       | 0                    | 0      |
| `"abc"`      | 1 + 1                | 2      |
| `"zaz"`      | 25 + 25              | 50     |
| `"hello"`    | 3 + 7 + 0 + 3        | 13     |

## Edge Cases to Consider

* Minimum length string (`length = 2`)
* All characters are the same
* Characters at extreme ends (`'a'` and `'z'`)

## Common Test Cases

* Sequential characters
* Repeated characters
* Random character strings

## Common Mistakes to Avoid

* Forgetting to take absolute value
* Starting loop from index `0`
* Misinterpreting character difference logic

## Interview Relevance

* Tests understanding of ASCII values
* Evaluates simple string traversal
* Common warm-up string problem

## What This Problem Teaches

* Working with character encodings
* Efficient traversal of strings
* Translating mathematical definitions into code

## Key Takeaways

* Adjacent character relationships can be processed independently
* ASCII arithmetic simplifies character-based problems
* Linear traversal is optimal for fixed constraints

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic string manipulation and arithmetic operations, making it ideal for beginners and interview warm-ups.