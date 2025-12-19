# A. Petya and Strings

## Platform

Codeforces

## Problem Link

[A. Petya and Strings](https://codeforces.com/problemset/problem/112/A)

## Problem Statement

Petya loves comparing strings.
He compares two strings **lexicographically**, but the comparison is **case-insensitive**.

Given two strings of equal length consisting of uppercase and lowercase English letters, determine:

* Print `-1` if the first string is lexicographically smaller
* Print `1` if the first string is lexicographically greater
* Print `0` if both strings are equal

All comparisons must be done **without considering letter case**.

## Input Format

* The first line contains a string `s1`
* The second line contains a string `s2`

## Output Format

* Print a single integer: `-1`, `1`, or `0` based on the comparison result

## Constraints

* `1 ≤ length(s1), length(s2) ≤ 100`
* `length(s1) = length(s2)`
* Strings contain only English alphabet letters

## Examples

### Example 1

Input

```
aaaa
aaaA
```

Explanation
After converting both strings to the same case:

```
AAAA
AAAA
```

Both strings are equal.

Output

```
0
```

---

### Example 2

Input

```
abs
Abz
```

Explanation
Case-insensitive comparison:

```
ABS
ABZ
```

At index 2:

```
S < Z
```

Output

```
-1
```

---

## Approach

Character-by-character lexicographical comparison after case normalization.

## Intuition

* Lexicographical comparison works correctly only if characters are in the same case.
* By converting both strings to **uppercase**, each character can be compared directly using ASCII values.
* The first position where characters differ determines the result.
* If all characters match, the strings are equal.

## Algorithm Steps

* Read both strings
* Traverse both strings character by character
* Convert lowercase letters to uppercase using ASCII manipulation
* Compare characters at the same index
* Print result immediately upon mismatch
* If no mismatch is found, print `0`

## Visual Walkthrough

Input:

```
s1 = "aBc"
s2 = "AbD"
```

After conversion:

```
s1 = "ABC"
s2 = "ABD"
```

Comparison:

```
A == A
B == B
C < D  → result = -1
```

## Complexity Analysis

### Time Complexity

O(n)
Each character is processed exactly once.

### Space Complexity

O(1)
No extra data structures are used.

## Solution Explanation

The solution converts both strings to uppercase on the fly using ASCII value manipulation.
Lowercase letters (`'a'` to `'z'`) have ASCII values greater than `92`, so subtracting `32` converts them to uppercase.

Characters are compared immediately after conversion.
The first mismatch determines the lexicographical order, allowing early termination.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Strings to be compared
    string s1, s2;

    // Read both strings
    cin >> s1 >> s2;

    // Traverse each character of the strings
    for (int i = 0; i < s1.length(); i++) {

        // Convert lowercase characters to uppercase using ASCII values
        // ASCII value of 'a' is 97, 'A' is 65
        // Difference between lowercase and uppercase is 32
        if (s1[i] > 92)
            s1[i] -= 32;

        if (s2[i] > 92)
            s2[i] -= 32;

        // Lexicographical comparison
        if (s1[i] < s2[i]) {
            cout << -1;
            return 0;
        }

        if (s1[i] > s2[i]) {
            cout << 1;
            return 0;
        }
    }

    // If all characters are equal
    cout << 0;
    return 0;
}
```

## Test Cases Analysis

| s1   | s2   | Comparison Result |
| ---- | ---- | ----------------- |
| aaaa | AAAA | 0                 |
| abc  | abD  | -1                |
| zzz  | aaa  | 1                 |
| Aa   | aA   | 0                 |

## Edge Cases to Consider

* Strings already in the same case
* Strings differing at the first character
* Strings differing at the last character

## Common Test Cases

* Mixed uppercase and lowercase input
* Completely identical strings
* Strings with one differing character

## Common Mistakes to Avoid

* Comparing characters without normalizing case
* Using incorrect ASCII boundaries
* Forgetting early termination on mismatch

## Interview Relevance

* Tests string traversal and comparison
* Reinforces ASCII value understanding
* Common beginner string manipulation problem

## What This Problem Teaches

* Case normalization techniques
* Efficient lexicographical comparison
* Importance of early exit conditions

## Key Takeaways

* Always normalize input before comparison
* ASCII arithmetic can simplify character handling
* Early termination improves clarity and efficiency

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on string handling, ASCII manipulation, and logical comparison, making it a standard beginner and interview warm-up problem.