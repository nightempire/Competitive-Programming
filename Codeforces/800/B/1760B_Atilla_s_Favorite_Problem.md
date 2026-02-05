# B_Atilla_s_Favorite_Problem

## Platform

Codeforces

## Problem Link

[B. Atilla’s Favorite Problem](https://codeforces.com/problemset/problem/1760/B)

## Problem Statement

You are given multiple test cases.
In each test case:

* An integer `n`, the length of a string
* A string `s` consisting of lowercase English letters

Atilla defines the **value of a string** as the position of the **lexicographically largest character** in the English alphabet, where:

```
'a' → 1
'b' → 2
...
'z' → 26
```

Your task is to compute and print the value of the given string for each test case.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`
  * The second line contains a string `s` of length `n`

## Output Format

For each test case, output a single integer — the value of the string.

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 100`
* `s` consists only of lowercase English letters

## Examples

### Example 1

Input

```
3
3
abc
5
azaza
1
z
```

Explanation

* Test case 1:

  * Largest character → `'c'`
  * Position → `3`
* Test case 2:

  * Largest character → `'z'`
  * Position → `26`
* Test case 3:

  * Largest character → `'z'`
  * Position → `26`

Output

```
3
26
26
```

### Example 2

Input

```
2
4
code
6
forces
```

Explanation

* `"code"` → largest character `'o'` → `15`
* `"forces"` → largest character `'s'` → `19`

Output

```
15
19
```

## Approach

**Single-pass maximum character detection**

## Intuition

The value of the string depends **only on its maximum character**.

Since all characters are lowercase English letters:

* Finding the maximum character lexicographically is sufficient
* Its position can be computed using ASCII arithmetic

There is no need for sorting or extra data structures.

## Algorithm Steps

* Read integer `t`
* For each test case:

  * Read integer `n` and string `s`
  * Initialize a variable `mx` to `'a'`
  * Traverse the string:

    * Update `mx` if a larger character is found
  * Output `mx - 'a' + 1`

## Visual Walkthrough

### Test Case 1

Input:

```
s = "baca"
```

Traversal:

```
b → mx = b
a → mx = b
c → mx = c
a → mx = c
```

Final maximum character:

```
'c'
```

Value:

```
'c' - 'a' + 1 = 3
```

---

### Test Case 2

Input:

```
s = "leetcode"
```

Maximum character:

```
't'
```

Value:

```
't' - 'a' + 1 = 20
```

---

### Test Case 3

Input:

```
s = "a"
```

Maximum character:

```
'a'
```

Value:

```
1
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each character in the string is visited exactly once.

### Space Complexity

**O(1)**

Only a single character variable is used.

## Solution Explanation

The solution scans the string to identify the lexicographically largest character.
Since lowercase letters are contiguous in ASCII, converting a character to its alphabetical position is straightforward using subtraction.

This results in a clean, fast, and reliable solution.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int n;
        cin >> n;

        string s;
        cin >> s;

        // Track the maximum character
        char mx = 'a';

        // Traverse the string
        for (char ch : s) {
            if (ch > mx) {
                mx = ch;
            }
        }

        // Convert character to alphabet position
        cout << mx - 'a' + 1 << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | String | Max Character | Output |
| --------- | ------ | ------------- | ------ |
| 1         | abc    | c             | 3      |
| 2         | azaza  | z             | 26     |
| 3         | z      | z             | 26     |
| 4         | code   | o             | 15     |
| 5         | forces | s             | 19     |

## Edge Cases to Consider

* String of length `1`
* All characters are the same
* Character `'z'` present anywhere in the string

## Common Test Cases

* Random lowercase strings
* Strings with repeated maximum characters
* Minimum-length strings

## Common Mistakes to Avoid

* Sorting the string unnecessarily
* Incorrect ASCII-to-index conversion
* Forgetting that indexing starts from `'a'`

## Interview Relevance

* Tests basic string traversal
* Evaluates understanding of character encoding
* Common warm-up problem in interviews

## What This Problem Teaches

* Efficient maximum-finding techniques
* Using ASCII arithmetic correctly
* Avoiding overengineering simple problems

## Key Takeaways

* Only required information should be computed
* Linear scans are often sufficient
* Character arithmetic simplifies many problems

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes clarity, correctness, and efficient use of basic programming constructs.