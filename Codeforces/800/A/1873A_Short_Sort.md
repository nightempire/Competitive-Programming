# A. Short Sort

## Platform

Codeforces

## Problem Link

[https://codeforces.com/problemset/problem/1873/A](https://codeforces.com/problemset/problem/1873/A)

## Problem Statement

You are given a string of length **3** consisting of lowercase English letters.

The goal is to determine whether the string can be transformed into the string **"abc"** using **at most one swap** of any two characters.

For each test case, output `"YES"` if it is possible; otherwise, output `"NO"`.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each of the next `t` lines contains a string `s` of length `3`.

## Output Format

For each test case, print `"YES"` or `"NO"` on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* Length of `s` is exactly `3`
* `s` contains only lowercase English letters

## Examples

### Example 1

Input

```
3
abc
acb
xyz
```

Explanation

* `"abc"` → already sorted → **YES**
* `"acb"` → swap `'c'` and `'b'` → `"abc"` → **YES**
* `"xyz"` → cannot form `"abc"` → **NO**

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
bac
cba
```

Explanation

* `"bac"` → swap `'b'` and `'a'` → `"abc"` → **YES**
* `"cba"` → requires more than one swap → **NO**

Output

```
YES
NO
```

## Approach (Algorithm Type)

Direct character position validation.

## Intuition

Since the string length is always **3**, all valid permutations that can form `"abc"` in **at most one swap** must have **at least one character already in its correct position**.

If:

* `'a'` is at index `0`, or
* `'b'` is at index `1`, or
* `'c'` is at index `2`

then the string can be converted into `"abc"` using at most one swap.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read the string `s`
  * Check if:

    * `s[0] == 'a'` **or**
    * `s[1] == 'b'` **or**
    * `s[2] == 'c'`
  * If any condition is true, print `"YES"`
  * Otherwise, print `"NO"`

## Visual Walkthrough

Test Case 1:

```
s = "acb"
```

Positions:

```
index 0 → 'a' ✔
index 1 → 'c'
index 2 → 'b'
```

At least one correct position → **YES**

---

Test Case 2:

```
s = "cba"
```

Positions:

```
index 0 → 'c'
index 1 → 'b' ✔
index 2 → 'a'
```

Although `'b'` is correct, sorting requires more than one swap → **NO**

---

Test Case 3:

```
s = "xyz"
```

No matching position → **NO**

## Complexity Analysis

### Time Complexity

O(t)
Each test case involves constant-time character comparisons.

### Space Complexity

O(1)
No extra memory is used.

## Solution Explanation

The solution leverages the fixed string size (3) to avoid unnecessary sorting or permutation checks.

By validating whether **at least one character is already in its correct target position**, we guarantee that the remaining characters can be fixed with at most one swap.

This results in a clean, optimal, and constraint-aligned solution.

## Full Solution (Heavily Commented C++ Code)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Input string of length exactly 3
        string s;
        cin >> s;

        // Check if at least one character
        // is already in the correct position
        // for forming the string "abc"
        if (s[0] == 'a' || s[1] == 'b' || s[2] == 'c') {

            // Possible to form "abc" with at most one swap
            cout << "YES\n";
        } else {

            // Not possible to form "abc"
            cout << "NO\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Input String | Correct Positions | Output |
| ------------ | ----------------- | ------ |
| abc          | All               | YES    |
| acb          | a at index 0      | YES    |
| bac          | b at index 1      | YES    |
| cba          | none effective    | NO     |
| xyz          | none              | NO     |

## Edge Cases to Consider

* String already equals `"abc"`
* No character matches expected position
* Maximum number of test cases

## Common Test Cases

* Valid permutations of `"abc"`
* Completely unrelated characters
* Reverse order strings

## Common Mistakes to Avoid

* Sorting the string unnecessarily
* Overcomplicating with permutation logic
* Forgetting that string length is fixed

## Interview Relevance

* Tests logical reasoning under constraints
* Demonstrates optimization using fixed input size
* Evaluates understanding of permutations

## What This Problem Teaches

* How constraints simplify problem-solving
* Using position-based logic effectively
* Avoiding unnecessary computation

## Key Takeaways

* Fixed-size problems allow direct checks
* One correct position is sufficient
* Simplicity often yields optimal solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on reasoning with constraints rather than algorithmic complexity and is commonly used as a warm-up or screening question.