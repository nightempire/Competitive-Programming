# A_Short_Substrings

## Platform

Codeforces

## Problem Link

[A. Short Substrings](https://codeforces.com/problemset/problem/1367/A)

## Problem Statement

You are given a string `s` that was formed in a specific way:

* Start with a hidden original string `t`
* Create `s` by taking:

  * the first two characters of `t`
  * then for every next character of `t`, append it together with an extra character

As a result, the string `s` contains **redundant characters**.

Your task is to reconstruct and print the **original string `t`** from the given string `s`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case consists of a single string `s`.

## Output Format

For each test case, print the reconstructed original string.

## Constraints

* `1 ≤ t ≤ 1000`
* Length of string `s` is even
* `2 ≤ |s| ≤ 100`
* String `s` contains only lowercase English letters

## Examples

### Example 1

Input

```
3
abba
acbac
aaaa
```

Explanation

* Test case 1
  `s = "abba"`
  Original string: `"aba"`

* Test case 2
  `s = "acbac"`
  Original string: `"abc"`

* Test case 3
  `s = "aaaa"`
  Original string: `"aaa"`

Output

```
aba
abc
aaa
```

### Example 2

Input

```
1
codeforces
```

Explanation

Taking the first two characters and then every second character afterward reconstructs the original string.

Output

```
codeforces
```

## Approach (Algorithm Name / Type)

**Index-Based String Reconstruction**

## Intuition

The construction rule ensures that:

* The **first two characters** of `s` always belong to the original string
* Starting from index `3`, **every second character** represents the next original character

By skipping the redundant characters, we can rebuild the original string efficiently.

## Algorithm Steps

* Read the number of test cases
* For each test case:

  * Read the string `s`
  * Print `s[0]` and `s[1]`
  * Traverse the string starting from index `3`
  * Print every character at odd indices (`i += 2`)
  * Move to the next test case

## Visual Walkthrough

### Test Case 1

Input

```
s = "abba"
```

Index mapping

```
Index:   0 1 2 3
Chars:   a b b a
```

Reconstruction

```
Take s[0] → a
Take s[1] → b
Take s[3] → a
```

Result

```
"aba"
```

---

### Test Case 2

Input

```
s = "acbac"
```

Index mapping

```
Index:   0 1 2 3 4
Chars:   a c b a c
```

Reconstruction

```
s[0], s[1], s[3]
```

Result

```
"abc"
```

---

### Test Case 3

Input

```
s = "aaaa"
```

Reconstruction

```
a a a
```

Result

```
"aaa"
```

## Complexity Analysis

### Time Complexity

**O(n)**
Each character of the string is processed once.

### Space Complexity

**O(1)**
No extra memory is used beyond basic variables.

## Solution Explanation

The solution leverages the known structure of the constructed string.
By selecting the first two characters and then skipping every alternate character, we remove the redundant information and retrieve the original string efficiently.

This avoids unnecessary string manipulation or auxiliary data structures.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Input string formed with redundant characters
        string s;
        cin >> s;

        // The first two characters always belong to the original string
        cout << s[0] << s[1];

        // Starting from index 3, every second character
        // corresponds to the next original character
        for (int i = 3; i < s.size(); i += 2) {

            // Append the valid character
            cout << s[i];
        }

        // Move to the next output line
        cout << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input String | Output     | Reasoning                   |
| ------------ | ---------- | --------------------------- |
| abba         | aba        | Take indices 0, 1, 3        |
| acbac        | abc        | Skip redundant characters   |
| aaaa         | aaa        | All characters are the same |
| codeforces   | codeforces | Pattern still holds         |

## Edge Cases to Consider

* Minimum length string (`|s| = 2`)
* Strings with repeated characters
* Single test case input

## Common Test Cases

* Alternating characters
* All characters identical
* Mixed character strings

## Common Mistakes to Avoid

* Starting the loop from the wrong index
* Using incorrect step size in the loop
* Forgetting to print the first two characters

## Interview Relevance

* Tests understanding of string indexing
* Evaluates ability to reverse a construction process
* Common problem for assessing string manipulation skills

## What This Problem Teaches

* Identifying and leveraging input patterns
* Efficient string traversal
* Avoiding unnecessary memory usage

## Key Takeaways

* Understanding the problem construction simplifies the solution
* Index-based traversal is powerful and efficient
* Pattern recognition is crucial in string problems

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on string indexing and pattern observation, making it ideal for beginners and competitive programming practice.