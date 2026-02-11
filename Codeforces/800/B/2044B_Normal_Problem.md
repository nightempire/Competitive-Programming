# 2044B_Normal_Problem

## Platform

Codeforces

## Problem Link

[B. Normal Problem](https://codeforces.com/problemset/problem/2044/B)

## Problem Statement

You are given a string `s` consisting only of the characters:

```
'p', 'q', 'w'
```

Your task is to transform the string as follows:

* Reverse the string.
* Replace:

  * `'p'` with `'q'`
  * `'q'` with `'p'`
  * `'w'` remains `'w'`

Print the transformed string for each test case.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * A string `s`.

## Output Format

* For each test case, print the transformed string on a new line.

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ |s| ≤ 100`
* `s[i] ∈ {'p', 'q', 'w'}`

## Examples

### Example 1

Input

```
1
pqw
```

Explanation

Original: `"pqw"`

Reverse: `"wqp"`

Character replacement:

```
'w' → 'w'
'q' → 'p'
'p' → 'q'
```

Result:

```
wpq
```

Output

```
wpq
```

---

### Example 2

Input

```
1
ppqq
```

Explanation

Original: `"ppqq"`

Reverse: `"qqpp"`

Replacement:

```
'q' → 'p'
'q' → 'p'
'p' → 'q'
'p' → 'q'
```

Result:

```
ppqq
```

Output

```
ppqq
```

---

### Example 3

Input

```
1
w
```

Explanation

Single character remains unchanged.

Output

```
w
```

## Approach

**Reverse Traversal with Character Mapping**

## Intuition

The transformation consists of two independent operations:

* Reverse the string.
* Apply a character mapping rule.

Instead of explicitly reversing the string, we can:

* Traverse the string from the last character to the first.
* Apply character substitution during traversal.
* Print the result directly.

This avoids creating extra intermediate strings.

## Algorithm Steps

* Read number of test cases `t`.
* For each test case:

  * Read string `s`.
  * Traverse the string from index `n - 1` to `0`.
  * For each character:

    * If `'p'`, print `'q'`
    * If `'q'`, print `'p'`
    * Else print `'w'`
  * Print newline.

## Visual Walkthrough

### Case 1: `"pqw"`

```
Reverse order: w q p

Mapping:
w → w
q → p
p → q

Result: wpq
```

---

### Case 2: `"qp"`

```
Reverse order: p q

Mapping:
p → q
q → p

Result: qp
```

---

### Case 3: `"www"`

```
Reverse order: w w w
Mapping: w → w
Result: www
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each character is processed once.

### Space Complexity

**O(1)**

No additional data structures are used.

## Solution Explanation

The solution combines string reversal and character substitution in a single loop.

By iterating backward:

* The reversal is handled implicitly.
* The mapping is applied immediately.

This ensures efficiency and simplicity.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        string s;
        cin >> s;

        int n = s.length();

        // Traverse from end to beginning (reverse order)
        for (int i = n - 1; i >= 0; i--) {

            // Apply character mapping
            if (s[i] == 'p')
                cout << 'q';
            else if (s[i] == 'q')
                cout << 'p';
            else
                cout << 'w';
        }

        cout << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input  | Reversed | Final Output |
| ------ | -------- | ------------ |
| `pqw`  | `wqp`    | `wpq`        |
| `ppqq` | `qqpp`   | `ppqq`       |
| `w`    | `w`      | `w`          |
| `qpw`  | `wpq`    | `wpq`        |

## Edge Cases to Consider

* Single-character string
* All characters same
* Mixed character patterns
* Multiple test cases

## Common Test Cases

* Alternating `p` and `q`
* Strings with only `w`
* Palindromic strings

## Common Mistakes to Avoid

* Forgetting to reverse the string
* Incorrect character mapping
* Printing characters in wrong order

## Interview Relevance

* Tests string manipulation skills
* Evaluates character transformation logic
* Reinforces reverse traversal technique

## What This Problem Teaches

* Efficient string processing
* Combining multiple operations in one traversal
* Careful implementation of mapping rules

## Key Takeaways

* Reverse traversal can avoid extra memory usage
* Character substitution problems require careful mapping
* Simplicity leads to clean solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It involves straightforward string manipulation and conditional checks, making it ideal for beginner-level competitive programming practice.