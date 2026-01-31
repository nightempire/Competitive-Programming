# A. Skibidus and Amog’u

## Platform

Codeforces

## Problem Link

[A. Skibidus and Amog’u](https://codeforces.com/problemset/problem/2065/A)

## Problem Statement

You are given a string `s` for each test case.

The task is to **modify the last two characters of the string** so that:

* The second last character becomes `'i'`
* The last character becomes `'u'`

After performing this transformation, output the modified string.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * A single string `s`

## Output Format

For each test case, output the transformed string on a new line.

## Constraints

* `1 ≤ t ≤ 10⁴`
* `2 ≤ |s| ≤ 100`
* `s` consists of lowercase English letters

## Examples

### Example 1

Input

```
3
skibidus
amogu
hello
```

Explanation

* `"skibidus"` → replace last two characters → `"skibidiu"`
* `"amogu"` → replace last two characters → `"amoiu"`
* `"hello"` → replace last two characters → `"helio"`

Output

```
skibidiu
amoiu
helio
```

## Approach

**Direct string manipulation**

## Intuition

The problem guarantees that the string length is at least 2.

Therefore, the last two positions of the string can always be accessed safely and overwritten directly without affecting the rest of the string.

No additional checks or iterations are required.

## Algorithm Steps

* Read the number of test cases.
* For each test case:

  * Read the string `s`.
  * Determine its length `n`.
  * Replace:

    * `s[n − 2]` with `'i'`
    * `s[n − 1]` with `'u'`
  * Output the modified string.

## Visual Walkthrough

### Case 1

```
Original: skibidus
Indexes : 01234567
```

Replace:

```
s[6] = 'i'
s[7] = 'u'
```

Result:

```
skibidiu
```

---

### Case 2

```
Original: hello
```

Replace:

```
lo → iu
```

Result:

```
helio
```

## Complexity Analysis

### Time Complexity

**O(|s|)** per test case

Only constant-time character replacement is performed, but output requires printing the entire string.

### Space Complexity

**O(1)**

The string is modified in place with no extra memory usage.

## Solution Explanation

The solution directly accesses the last two characters of the string and replaces them with fixed characters.

Since the string length is guaranteed to be at least 2, no boundary checks are required.
This makes the implementation straightforward and efficient.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while (t--) {

        // Input string
        string s;
        cin >> s;

        // Length of the string
        int n = s.length();

        // Replace last two characters
        s[n - 2] = 'i';
        s[n - 1] = 'u';

        // Output the modified string
        cout << s << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input String | Output String |
| ------------ | ------------- |
| skibidus     | skibidiu      |
| amogu        | amoiu         |
| hi           | iu            |
| hello        | helio         |

## Edge Cases to Consider

* Minimum length string (`|s| = 2`)
* Strings with repeated characters
* Multiple test cases

## Common Test Cases

* Standard words
* Short strings
* Long strings near constraint limits

## Common Mistakes to Avoid

* Modifying incorrect indices
* Forgetting to print a newline after each test case
* Assuming string length less than 2

## Interview Relevance

* Tests basic string manipulation
* Evaluates indexing correctness
* Simple implementation accuracy

## What This Problem Teaches

* Safe character replacement in strings
* Working with string indices
* Attention to problem guarantees

## Key Takeaways

* Problem constraints can simplify logic
* Direct manipulation is often optimal
* Always respect index boundaries

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It requires basic understanding of strings and indexing, making it ideal for beginners and quick contest problems.