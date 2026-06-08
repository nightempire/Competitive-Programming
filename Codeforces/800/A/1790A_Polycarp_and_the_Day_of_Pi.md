## 1790A. Polycarp and the Day of Pi

## Platform

Codeforces

## Problem Link

[A. Polycarp and the Day of Pi](https://codeforces.com/problemset/problem/1790/A)

## Problem Statement

Polycarp loves the number π (Pi).

He wrote down the first digits of π:

```text
314159265358979323846264338327
```

You are given a string `s` consisting of digits.

Your task is to determine the length of the longest prefix of `s` that matches the corresponding prefix of the digits of π.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains a string `s`.

## Output Format

* For each test case, print a single integer — the length of the longest matching prefix with π.

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ |s| ≤ 30`
* `s` consists only of digits.

## Examples

### Example 1

Input

```text
3
314159
31416
12345
```

Explanation

#### Test Case 1

String:

```text
314159
```

Pi prefix:

```text
314159
```

All digits match.

Output:

```text
6
```

---

#### Test Case 2

String:

```text
31416
```

Comparison:

```text
Pi : 3 1 4 1 5
Str: 3 1 4 1 6
                ✗
```

Matching prefix length:

```text
4
```

Output:

```text
4
```

---

#### Test Case 3

String:

```text
12345
```

Comparison:

```text
Pi : 3 ...
Str: 1 ...
     ✗
```

Matching prefix length:

```text
0
```

Output

```text
0
```

## Approach

String Comparison (Prefix Matching)

## Intuition

The digits of π are fixed:

```text
314159265358979323846264338327
```

For each test case:

* Compare the given string with π digit by digit.
* Stop at the first mismatch.
* The index where comparison stops equals the length of the matching prefix.

## Algorithm Steps

* Store the first 30 digits of π in a string.
* Read `t`.
* For each test case:

  * Read string `s`.
  * Start from index `0`.
  * Compare `s[i]` with `pi[i]`.
  * Continue while both digits are equal.
  * Stop at the first mismatch.
  * Print the number of matched digits.

## Visual Walkthrough

### Case 1

```text
s = "314159"
```

Comparison:

```text
Pi : 3 1 4 1 5 9
s  : 3 1 4 1 5 9
```

All digits match.

Answer:

```text
6
```

---

### Case 2

```text
s = "31416"
```

Comparison:

```text
Pi : 3 1 4 1 5
s  : 3 1 4 1 6
              ✗
```

Answer:

```text
4
```

---

### Case 3

```text
s = "31415926"
```

Comparison:

```text
Pi : 3 1 4 1 5 9 2 6
s  : 3 1 4 1 5 9 2 6
```

All digits match.

Answer:

```text
8
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Where `n` is the length of the input string.

Each character is compared at most once.

### Space Complexity

**O(1)**

Only the fixed Pi string and a few variables are used.

## Solution Explanation

The solution stores the first 30 digits of π in a string.

For every test case:

* Compare the input string with π from left to right.
* Continue while the characters match.
* The moment a mismatch occurs, stop.
* The current index represents the length of the matching prefix.

This directly follows the problem statement and is the most efficient approach.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // First 30 digits of Pi
    string a = "314159265358979323846264338327";

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input string
        string b;
        cin >> b;

        // Length of input string
        int n = b.size();

        // Current matching index
        int i = 0;

        // Compare with Pi digits
        while(i < n && a[i] == b[i]) {
            i++;
        }

        // Length of matching prefix
        cout << i << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input String | Matching Prefix | Output |
| ------------ | --------------- | ------ |
| 314159       | 314159          | 6      |
| 31416        | 3141            | 4      |
| 12345        | ""              | 0      |
| 3            | 3               | 1      |
| 314159265    | 314159265       | 9      |

## Edge Cases to Consider

* First digit does not match.
* Entire string matches π.
* String length is `1`.
* Mismatch occurs at the last character.
* Maximum allowed string length.

## Common Test Cases

* Exact prefix of π.
* Completely different string.
* Single-digit input.
* Partial match followed by mismatch.
* Full 30-digit match.

## Common Mistakes to Avoid

* Continuing comparison after the first mismatch.
* Using the wrong Pi digit sequence.
* Accessing indices beyond the string length.

## Interview Relevance

* Tests basic string processing.
* Demonstrates prefix matching.
* Reinforces character-by-character comparison techniques.

## What This Problem Teaches

* Prefix comparison between strings.
* Early termination for efficiency.
* Working with fixed reference strings.

## Key Takeaways

* Prefix matching problems are often solved with a simple linear scan.
* Stop immediately at the first mismatch.
* Fixed reference strings simplify implementation.

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The problem requires only straightforward character-by-character comparison against a predefined string representing the digits of π. The main task is implementing the prefix matching correctly.