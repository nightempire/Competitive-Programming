# A_Trippi_Troppi

## Platform

Codeforces

## Problem Link

[A. Trippi Troppi](https://codeforces.com/problemset/problem/1915/A)

## Problem Statement

You are given multiple test cases.
In each test case, three strings are provided.

Your task is to form a new string by taking the **first character of each of the three strings**, in the same order, and outputting the resulting string.

Each test case is independent.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * A single line contains **three strings** separated by spaces.

## Output Format

For each test case, output a string consisting of **exactly three characters**, formed by:

* the first character of the first string
* the first character of the second string
* the first character of the third string

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* Each string has a length of at least `1`
* Strings contain lowercase English letters only

## Examples

### Example 1

Input

```
2
trippi troppi trappa
code forces round
```

Explanation

* Test case 1:

  * First characters → `t`, `t`, `t`
  * Output → `ttt`
* Test case 2:

  * First characters → `c`, `f`, `r`
  * Output → `cfr`

Output

```
ttt
cfr
```

### Example 2

Input

```
1
a b c
```

Explanation

* First characters → `a`, `b`, `c`
* Output → `abc`

Output

```
abc
```

## Approach

Direct character extraction using string indexing.

## Intuition

Only the **first character** of each string matters.
There is no need to process or analyze the remaining characters.

For every test case:

* Read three strings
* Access index `0` of each string
* Concatenate and print them

This keeps the solution simple, efficient, and easy to reason about.

## Algorithm Steps

* Read integer `t`
* Repeat for each test case:

  * Read three strings
  * Extract the first character from each string
  * Print the concatenated result
* End execution

## Visual Walkthrough

### Test Case 1

Input strings:

```
"hello" "world" "code"
```

Character extraction:

```
h  w  c
```

Output:

```
hwc
```

---

### Test Case 2

Input strings:

```
"a" "bc" "def"
```

Character extraction:

```
a  b  d
```

Output:

```
abd
```

---

### Test Case 3

Input strings:

```
"one" "two" "three"
```

Character extraction:

```
o  t  t
```

Output:

```
ott
```

## Complexity Analysis

### Time Complexity

**O(t)**

Each test case performs:

* Constant-time string reads
* Constant-time character access

Hence, the total time grows linearly with the number of test cases.

### Space Complexity

**O(1)**

Only a fixed number of strings and characters are stored at any time.
No additional memory proportional to input size is used.

## Solution Explanation

The solution processes each test case independently.
By leveraging the fact that strings in C++ allow direct indexing, the first character of each string can be accessed in constant time.

The extracted characters are printed consecutively, forming the required output for each test case.

This approach avoids unnecessary computations and adheres exactly to the problem constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Read the number of test cases
    int t;
    cin >> t;

    // Loop over all test cases
    while (t--) {

        // Array to store the three input strings
        string s[3];

        // Read the three strings
        cin >> s[0] >> s[1] >> s[2];

        // Output the first character of each string
        // s[i][0] directly accesses the first character
        cout << s[0][0] << s[1][0] << s[2][0] << '\n';
    }

    // Indicate successful program termination
    return 0;
}
```

## Test Cases Analysis

| Test Case | Input Strings        | Extracted Characters | Output |
| --------- | -------------------- | -------------------- | ------ |
| 1         | trippi troppi trappa | t t t                | ttt    |
| 2         | code forces round    | c f r                | cfr    |
| 3         | a b c                | a b c                | abc    |
| 4         | hello world cpp      | h w c                | hwc    |

## Edge Cases to Consider

* Strings of length `1`
* Minimum number of test cases (`t = 1`)
* All strings starting with the same character

## Common Test Cases

* Three single-character strings
* Strings with varying lengths
* Multiple test cases with mixed inputs

## Common Mistakes to Avoid

* Accessing incorrect indices instead of index `0`
* Forgetting to print a newline after each test case
* Assuming strings have a minimum length greater than 1

## Interview Relevance

* Tests understanding of string handling
* Reinforces indexing concepts
* Evaluates basic input-output discipline

## What This Problem Teaches

* Efficient use of strings
* Importance of focusing only on required data
* Clean and minimal logic for simple tasks

## Key Takeaways

* Not all problems require complex logic
* Direct access operations can simplify solutions
* Reading problem constraints carefully saves effort

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes clarity, correct input handling, and basic string operations rather than algorithmic complexity.