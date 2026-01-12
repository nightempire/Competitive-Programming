# A_Love_Story

## Platform

Codeforces

## Problem Link

[A. Love Story](https://codeforces.com/problemset/problem/1829/A)

## Problem Statement

You are given a fixed string **"codeforces"**.
For each test case, another string of the same length is provided.

Your task is to determine **how many characters differ** between the given string and `"codeforces"` at the **same index positions**.

In other words, count the number of positions where the two strings do **not match**.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains a string `s` of length 10.

## Output Format

For each test case, output a single integer representing the number of mismatched characters compared to `"codeforces"`.

## Constraints

* `1 ≤ t ≤ 1000`
* Length of each string `s` is exactly `10`
* Strings contain only lowercase English letters

## Examples

### Example 1

Input

```
3
codeforces
codeforcse
codexorces
```

Explanation

* Test case 1
  All characters match → mismatches = 0

* Test case 2
  Characters at index 8 and 9 are swapped
  Mismatches = 2

* Test case 3
  Character at index 4 differs (`x` instead of `f`)
  Mismatches = 1

Output

```
0
2
1
```

### Example 2

Input

```
1
aaaaaaaaaa
```

Explanation
None of the characters match `"codeforces"`.

Output

```
10
```

## Approach (Algorithm Name / Type)

**Direct String Comparison (Index-wise Traversal)**

## Intuition

Since both strings have a fixed and equal length, the simplest and most efficient approach is to compare characters **position by position**.

Every time a character in the input string differs from the corresponding character in `"codeforces"`, we increment a counter.

This avoids unnecessary data structures or complex logic.

## Algorithm Steps

* Store the reference string `"codeforces"`.
* Read the number of test cases.
* For each test case:

  * Read the input string.
  * Initialize a mismatch counter.
  * Traverse both strings from index `0` to `9`.
  * Increment the counter whenever characters at the same index differ.
  * Print the counter.

## Visual Walkthrough

### Test Case 1

Reference

```
c o d e f o r c e s
```

Input

```
c o d e f o r c e s
```

Comparison
All positions match → mismatches = 0

---

### Test Case 2

Reference

```
c o d e f o r c e s
```

Input

```
c o d e f o r c s e
```

Mismatched positions

```
Index 8: e ≠ s
Index 9: s ≠ e
```

Total mismatches = 2

---

### Test Case 3

Reference

```
c o d e f o r c e s
```

Input

```
c o d e x o r c e s
```

Mismatched position

```
Index 4: f ≠ x
```

Total mismatches = 1

## Complexity Analysis

### Time Complexity

**O(t × 10)**
Each test case compares exactly 10 characters, which is constant time.

### Space Complexity

**O(1)**
Only a few variables are used; no extra memory proportional to input size.

## Solution Explanation

The solution uses a fixed reference string and compares it directly with each input string.
By iterating through each character index and counting mismatches, the problem is solved efficiently and clearly.

This approach is optimal given the fixed string length.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Reference string to compare against
    const string x = "codeforces";

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Counter to store number of mismatched characters
        int count = 0;

        // Input string for the current test case
        string s;
        cin >> s;

        // Compare each character of the input string
        // with the corresponding character in "codeforces"
        for (int i = 0; i < 10; i++) {

            // If characters at the same index differ,
            // increment the mismatch counter
            if (x[i] != s[i]) {
                count++;
            }
        }

        // Output the number of mismatches for this test case
        cout << count << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Input String | Expected Output | Reasoning                 |
| --------- | ------------ | --------------- | ------------------------- |
| 1         | codeforces   | 0               | All characters match      |
| 2         | codeforcse   | 2               | Two swapped characters    |
| 3         | aaaaaaaaaa   | 10              | No character matches      |
| 4         | codexorces   | 1               | Single character mismatch |

## Edge Cases to Consider

* Input string completely different from `"codeforces"`
* Input string exactly equal to `"codeforces"`
* Minimum number of test cases (`t = 1`)

## Common Test Cases

* One-character difference
* Multiple-character differences
* Fully matching string
* Fully mismatching string

## Common Mistakes to Avoid

* Comparing strings of different lengths
* Using incorrect loop bounds
* Forgetting to reset the mismatch counter for each test case

## Interview Relevance

* Tests understanding of string traversal
* Evaluates attention to index-based comparison
* Common pattern in string matching problems

## What This Problem Teaches

* Efficient character-by-character comparison
* Working with fixed-length strings
* Writing clean and readable loop logic

## Key Takeaways

* Fixed-size problems often allow constant-time solutions
* Direct comparison is usually better than complex logic
* Simplicity improves correctness and performance

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic string manipulation and logical comparison, making it suitable for beginners and competitive programming warm-ups.