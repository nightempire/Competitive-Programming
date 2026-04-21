## 2065B. Skibidus and Ohio

## Platform

Codeforces

## Problem Link

[Skibidus and Ohio](https://codeforces.com/problemset/problem/2065/B)

## Problem Statement

You are given a string `s`.

You are allowed to perform operations where you can remove characters under certain conditions. The goal is to determine the **minimum possible length** of the string after performing optimal operations.

The key observation is:

* If the string contains **at least one pair of adjacent equal characters**, the answer becomes `1`.
* Otherwise, no reduction is possible, and the answer remains the original length of the string.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains a string `s`.

## Output Format

* For each test case, print a single integer — the minimum possible length of the string.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ |s| ≤ 2 × 10^5`
* The total length of all strings does not exceed `2 × 10^5`

## Examples

### Example 1

Input

```
3
abba
abcd
aa
```

Explanation

* `abba` → contains `"bb"` → can reduce to length `1`
* `abcd` → no adjacent equal characters → remains `4`
* `aa` → adjacent equal characters → reduce to `1`

Output

```
1
4
1
```

---

### Example 2

Input

```
2
abcabc
zz
```

Explanation

* `abcabc` → no adjacent equal → remains `6`
* `zz` → adjacent equal → reduce to `1`

Output

```
6
1
```

---

### Example 3

Input

```
1
a
```

Explanation

* Single character → no adjacent pair → remains `1`

Output

```
1
```

## Approach

Linear Scan (Greedy Observation)

## Intuition

The presence of **two consecutive equal characters** is the decisive factor:

* If such a pair exists, the operations can ultimately reduce the string to length `1`.
* If no such pair exists, no operation helps reduce the string.

Thus, we only need to check for **adjacent duplicates**.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read string `s`
  * Initialize a flag as `false`
  * Traverse the string:

    * If `s[i] == s[i-1]`, set flag = `true` and break
  * If flag is true → print `1`
  * Else → print `length of s`

## Visual Walkthrough

### Case 1

```
s = "abba"
```

```
a b b a
    ↑ ↑  → adjacent equal → YES
Answer = 1
```

---

### Case 2

```
s = "abcd"
```

```
a b c d
(no equal adjacent characters)
Answer = 4
```

---

### Case 3

```
s = "aa"
```

```
a a
↑ ↑ → adjacent equal → YES
Answer = 1
```

## Complexity Analysis

### Time Complexity

**O(n) per test case**

Each string is scanned once.

### Space Complexity

**O(1)**

Only a boolean flag is used.

## Solution Explanation

The solution iterates through the string and checks for adjacent equal characters. The moment such a pair is found, it concludes that the string can be reduced to length `1`. Otherwise, the original length is returned.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input string
        string s;
        cin >> s;

        // Length of string
        int n = s.length();

        // Flag to check adjacent equal characters
        bool flag = false;

        // Traverse string
        for(int i = 1; i < n; i++) {

            // If adjacent characters are equal
            if(s[i - 1] == s[i]) {
                flag = true;
                break;
            }
        }

        // Output result
        // If found → answer is 1
        // Else → answer is length of string
        cout << (flag ? 1 : n) << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| String | Adjacent Equal Exists | Output |
| ------ | --------------------- | ------ |
| abba   | Yes                   | 1      |
| abcd   | No                    | 4      |
| aa     | Yes                   | 1      |
| a      | No                    | 1      |
| abcabc | No                    | 6      |

## Edge Cases to Consider

* Single character string
* All characters same
* No repeated characters
* Very large strings

## Common Test Cases

* Strings with exactly one adjacent duplicate
* Strings with multiple duplicates
* Strings with no duplicates
* Minimum size input

## Common Mistakes to Avoid

* Checking for non-adjacent duplicates instead of adjacent
* Forgetting to break early after finding a match
* Overcomplicating with unnecessary operations

## Interview Relevance

* Tests string traversal and observation skills
* Evaluates ability to simplify problem logic
* Common pattern recognition problem

## What This Problem Teaches

* Importance of identifying key conditions
* Simplifying problems using observations
* Efficient linear scans

## Key Takeaways

* Adjacent duplicates determine the outcome
* Early exit improves efficiency
* Always check for simpler patterns before complex logic

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The main requirement is recognizing that the existence of adjacent equal characters alone determines the final answer, making the implementation straightforward.