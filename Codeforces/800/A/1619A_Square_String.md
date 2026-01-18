# A_Square_String

## Platform

Codeforces

## Problem Link

[A. Square String](https://codeforces.com/problemset/problem/1619/A)

## Problem Statement

A string is called a **square string** if it can be divided into two equal halves such that both halves are **identical**.

You are given multiple test cases. For each test case, determine whether the given string is a square string or not.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains a single string `s`.

## Output Format

For each test case, print:

* `YES` if the string is a square string
* `NO` otherwise

Output is **case-sensitive** and must be printed on a new line for each test case.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ |s| ≤ 100`
* The string contains only lowercase English letters

## Examples

### Example 1

Input

```
3
abab
abcabc
aba
```

Explanation

* `abab` → split into `ab` and `ab` → identical → square string
* `abcabc` → split into `abc` and `abc` → identical → square string
* `aba` → length is odd → cannot be split equally → not a square string

Output

```
YES
YES
NO
```

### Example 2

Input

```
2
zzzz
abcd
```

Explanation

* `zzzz` → `zz` + `zz` → square string
* `abcd` → `ab` + `cd` → not identical

Output

```
YES
NO
```

## Approach

**String Comparison using Half-Splitting**

The solution verifies whether the string length is even and compares characters from the first half with the corresponding characters in the second half.

## Intuition

A square string must satisfy two conditions:

* The length of the string must be even
* The first half must be exactly the same as the second half

If either condition fails, the string cannot be a square string.

## Algorithm Steps

* Read the number of test cases.
* For each string:

  * Check if its length is odd.

    * If yes, print `NO`.
  * Otherwise:

    * Compare characters at index `i` and `i + n/2`.
    * If any mismatch occurs, print `NO`.
    * If all characters match, print `YES`.

## Visual Walkthrough

### Test Case 1

String: `abab`

```
First half  → a b
Second half → a b
```

Comparison:

```
a == a ✓
b == b ✓
```

Result: `YES`

---

### Test Case 2

String: `abcd`

```
First half  → a b
Second half → c d
```

Comparison:

```
a != c ✗
```

Result: `NO`

---

### Test Case 3

String: `aba`

```
Length is odd → cannot split equally
```

Result: `NO`

## Complexity Analysis

### Time Complexity

O(n) per test case

Each character in the first half of the string is compared once with its corresponding character in the second half.

### Space Complexity

O(1)

Only a few constant variables are used; no additional data structures are required.

## Solution Explanation

The solution efficiently determines whether a string is a square string by first eliminating invalid cases with odd lengths.
For valid lengths, it performs a direct character-by-character comparison between the two halves of the string.
This avoids unnecessary substring creation and ensures optimal performance.

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

        // Input string
        string s;
        cin >> s;

        // Length of the string
        int n = s.length();

        // If the length is odd, it cannot be a square string
        if (n & 1) {
            cout << "NO\n";
            continue;
        }

        // Flag to detect mismatch between halves
        bool flag = false;

        // Compare first half and second half
        for (int i = 0; i < n / 2; i++) {

            // Compare corresponding characters
            if (s[i] != s[i + n / 2]) {
                flag = true;
                break;
            }
        }

        // Output result based on comparison
        cout << (flag ? "NO\n" : "YES\n");
    }

    return 0;
}
```

## Test Cases Analysis

| String | Length | First Half | Second Half | Output |
| ------ | ------ | ---------- | ----------- | ------ |
| abab   | 4      | ab         | ab          | YES    |
| aba    | 3      | —          | —           | NO     |
| zzzz   | 4      | zz         | zz          | YES    |
| abcd   | 4      | ab         | cd          | NO     |

## Edge Cases to Consider

* String length is `1`
* String length is odd
* All characters are the same
* Large number of test cases

## Common Test Cases

* Repeating patterns like `aa`, `abab`, `xyzxyz`
* Non-matching halves like `abca`
* Minimal input size

## Common Mistakes to Avoid

* Forgetting to check for even length
* Comparing incorrect indices
* Using substring operations unnecessarily

## Interview Relevance

* Tests string manipulation fundamentals
* Reinforces index-based traversal
* Common warm-up question in coding interviews

## What This Problem Teaches

* Efficient string comparison
* Early elimination of invalid cases
* Writing clean and optimal condition checks

## Key Takeaways

* Even length is a prerequisite for square strings
* Direct character comparison is faster than substring creation
* Simple logic can solve problems efficiently

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic string handling and conditional logic, making it suitable for beginners and interview preparation.