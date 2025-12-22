# A. Boy or Girl

## Platform

Codeforces

## Problem Link

[A. Boy or Girl](https://codeforces.com/problemset/problem/236/A)

## Problem Statement

A username is given consisting of lowercase English letters.

According to the rules:

* If the number of **distinct characters** in the username is **odd**, print
  **`IGNORE HIM!`**
* If the number of **distinct characters** is **even**, print
  **`CHAT WITH HER!`**

Determine the correct output based on the given username.

## Input Format

* A single line containing a string `s` consisting of lowercase English letters.

## Output Format

* Print one of the following messages:

  * `CHAT WITH HER!`
  * `IGNORE HIM!`

## Constraints

* `1 ≤ length(s) ≤ 100`
* `s` contains only lowercase English letters (`a` to `z`)

## Examples

### Example 1

Input

```
wjmzbmr
```

Explanation
Distinct characters:

```
w, j, m, z, b, r → 6
```

Since `6` is even:

Output

```
CHAT WITH HER!
```

---

### Example 2

Input

```
xiaodao
```

Explanation
Distinct characters:

```
x, i, a, o, d → 5
```

Since `5` is odd:

Output

```
IGNORE HIM!
```

---

## Approach

Frequency counting using a fixed-size array.

## Intuition

* The English alphabet has only 26 lowercase letters.
* By counting how many **unique letters** appear in the string, the problem reduces to checking whether that count is odd or even.
* The actual frequency does not matter—only whether a character appears at least once.

## Algorithm Steps

* Read the input string
* Create a frequency array of size `26`
* Traverse the string and mark character occurrences
* Count how many characters appear at least once
* Check the parity (odd or even) of the count
* Print the corresponding message

## Visual Walkthrough

For input:

```
abac
```

Frequency presence:

```
a → present
b → present
c → present
```

Distinct character count:

```
3 (odd)
```

Decision:

```
Odd → IGNORE HIM!
```

## Complexity Analysis

### Time Complexity

O(n)
Each character in the string is processed once.

### Space Complexity

O(1)
The frequency array has a fixed size of 26.

## Solution Explanation

The solution uses a frequency array indexed by characters `'a'` to `'z'`.
Each character in the string increments its corresponding index.

After processing the string, the program counts how many characters have a frequency greater than zero.
If the count is odd, it prints `"IGNORE HIM!"`; otherwise, it prints `"CHAT WITH HER!"`.

This method is efficient, simple, and perfectly suited to the problem constraints.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Input string (username)
    string s;
    cin >> s;

    // Frequency array for 26 lowercase English letters
    int f[26] = {0};

    // Count frequency of each character
    for (char ch : s) {
        f[ch - 'a']++;
    }

    // Count how many distinct characters are present
    int count = 0;
    for (int i : f) {
        if (i > 0)
            count++;
    }

    // If the number of distinct characters is odd,
    // print "IGNORE HIM!", otherwise print "CHAT WITH HER!"
    cout << ((count & 1) ? "IGNORE HIM!" : "CHAT WITH HER!");

    return 0;
}
```

## Test Cases Analysis

| Input    | Distinct Characters | Count | Output         |
| -------- | ------------------- | ----- | -------------- |
| `a`      | a                   | 1     | IGNORE HIM!    |
| `ab`     | a, b                | 2     | CHAT WITH HER! |
| `abc`    | a, b, c             | 3     | IGNORE HIM!    |
| `aabbcc` | a, b, c             | 3     | IGNORE HIM!    |

## Edge Cases to Consider

* Single-character usernames
* All characters identical
* All 26 letters present exactly once

## Common Test Cases

* Short strings
* Strings with repeated characters
* Strings with all unique characters

## Common Mistakes to Avoid

* Counting total characters instead of distinct ones
* Forgetting to initialize the frequency array
* Using unnecessary data structures for such a small alphabet

## Interview Relevance

* Tests understanding of frequency counting
* Reinforces character-to-index mapping
* Common beginner problem in interviews and contests

## What This Problem Teaches

* Efficient handling of uniqueness checks
* Importance of fixed-size optimizations
* Using parity checks for decision making

## Key Takeaways

* Distinct counts often matter more than raw frequency
* Fixed alphabets enable O(1) space solutions
* Bitwise checks (`& 1`) are concise and effective

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic string processing and counting logic, making it ideal for beginners and competitive programming practice.