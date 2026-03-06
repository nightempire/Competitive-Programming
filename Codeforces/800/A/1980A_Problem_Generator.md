# A_Problem_Generator

## Platform

Codeforces

## Problem Link

[A. Problem Generator](https://codeforces.com/problemset/problem/1980/A)

## Problem Statement

A contest problem generator produces problems categorized by uppercase English letters.

You are given a string `s` of length `n` consisting of characters from `'A'` to `'G'`. Each character represents the **type of problem** generated.

For a contest, the organizer requires **exactly `m` problems of each type** (`A` through `G`).

Your task is to determine **how many additional problems must be generated** so that every problem type appears **at least `m` times**.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * The first line contains two integers `n` and `m`.
  * The second line contains a string `s` of length `n`.

## Output Format

For each test case, print a single integer — the **minimum number of additional problems needed**.

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n ≤ 100`
* `1 ≤ m ≤ 100`
* `s` consists only of characters from `'A'` to `'G'`.

## Examples

### Example 1

Input

```
1
7 2
ABCDEFG
```

Explanation

Frequency of problem types:

| Type | Count |
| ---- | ----- |
| A    | 1     |
| B    | 1     |
| C    | 1     |
| D    | 1     |
| E    | 1     |
| F    | 1     |
| G    | 1     |

Required count for each type = `2`.

Additional needed:

| Type | Needed |
| ---- | ------ |
| A    | 1      |
| B    | 1      |
| C    | 1      |
| D    | 1      |
| E    | 1      |
| F    | 1      |
| G    | 1      |

Total additional problems:

```
7
```

Output

```
7
```

---

### Example 2

Input

```
1
10 1
AABBBCCCDD
```

Explanation

Frequency:

| Type | Count |
| ---- | ----- |
| A    | 2     |
| B    | 3     |
| C    | 3     |
| D    | 2     |
| E    | 0     |
| F    | 0     |
| G    | 0     |

Required minimum per type = `1`.

Missing counts:

| Type | Needed |
| ---- | ------ |
| E    | 1      |
| F    | 1      |
| G    | 1      |

Total additional problems:

```
3
```

Output

```
3
```

---

### Example 3

Input

```
1
5 3
AAABB
```

Explanation

Frequency:

| Type | Count |
| ---- | ----- |
| A    | 3     |
| B    | 2     |
| C    | 0     |
| D    | 0     |
| E    | 0     |
| F    | 0     |
| G    | 0     |

Required count per type = `3`.

Additional needed:

| Type | Needed |
| ---- | ------ |
| B    | 1      |
| C    | 3      |
| D    | 3      |
| E    | 3      |
| F    | 3      |
| G    | 3      |

Total additional problems:

```
16
```

Output

```
16
```

## Approach

Frequency Counting (Fixed Alphabet Counting)

## Intuition

Since problem types range only from **A to G**, there are exactly **7 categories**.

The idea is:

* Count how many times each category appears.
* Compare each count with the required minimum `m`.
* If a category appears fewer than `m` times, we must generate additional problems.

For each category:

```
missing = max(0, m - frequency)
```

The total additional problems required is the sum of all missing counts.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read `n` and `m`.
  * Read string `s`.
  * Create an array `f[7]` to store frequency of letters `A–G`.
  * Iterate through the string:

    * Increment frequency using `f[ch - 'A']`.
  * Initialize `count = 0`.
  * For each category:

    * If `frequency < m`

      * Add `m - frequency` to `count`.
  * Print `count`.

## Visual Walkthrough

### Test Case 1

Input

```
s = ABCDEFG
m = 2
```

Frequencies

| Type | Count |
| ---- | ----- |
| A    | 1     |
| B    | 1     |
| C    | 1     |
| D    | 1     |
| E    | 1     |
| F    | 1     |
| G    | 1     |

Needed:

```
2 - 1 = 1 for each type
```

Total:

```
7
```

---

### Test Case 2

```
s = AABBBCCCDD
m = 1
```

Counts:

| Type | Count |
| ---- | ----- |
| A    | 2     |
| B    | 3     |
| C    | 3     |
| D    | 2     |
| E    | 0     |
| F    | 0     |
| G    | 0     |

Missing:

```
E → 1
F → 1
G → 1
```

Total:

```
3
```

---

### Test Case 3

```
s = AAABB
m = 3
```

Counts:

| Type | Count |
| ---- | ----- |
| A    | 3     |
| B    | 2     |
| C    | 0     |
| D    | 0     |
| E    | 0     |
| F    | 0     |
| G    | 0     |

Missing:

```
B → 1
C → 3
D → 3
E → 3
F → 3
G → 3
```

Total:

```
16
```

## Complexity Analysis

### Time Complexity

O(n)

Each character of the string is processed once to compute frequency.

Additional iteration over 7 categories is constant time.

### Space Complexity

O(1)

The frequency array has a fixed size of 7 elements.

## Solution Explanation

The program uses a **frequency array** of size 7 to count occurrences of each problem category.

For each character in the string:

```
index = ch - 'A'
```

This maps:

```
A → 0
B → 1
C → 2
...
G → 6
```

After counting frequencies, the program checks how many more problems are needed to reach the required count `m` for each category.

The final result is the sum of all required additions.

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

        // n = length of string
        // m = required number of problems per category
        int n, m;
        cin >> n >> m;

        // String representing generated problem types
        string s;
        cin >> s;

        // Frequency array for letters A to G
        // Total categories = 7
        int f[7] = {0};

        // Variable to store required additional problems
        int count = 0;

        // Count frequency of each problem type
        for (char ch : s) {

            // Convert character to index
            // A → 0, B → 1, ..., G → 6
            f[ch - 'A']++;
        }

        // Check each category
        for (int freq : f) {

            // If current frequency is less than required m
            // add the missing amount
            if (freq < m) {
                count += (m - freq);
            }
        }

        // Output total additional problems required
        cout << count << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| String     | m | Missing Problems |
| ---------- | - | ---------------- |
| ABCDEFG    | 2 | 7                |
| AABBBCCCDD | 1 | 3                |
| AAABB      | 3 | 16               |

## Edge Cases to Consider

* String contains only one type of problem
* `m = 1`
* All categories already satisfy the requirement
* String length smaller than required total

## Common Test Cases

* Balanced distribution across categories
* Only one category present
* Large `m` relative to `n`
* Multiple test cases with small strings

## Common Mistakes to Avoid

* Forgetting that categories range only from **A to G**
* Incorrect index calculation (`ch - 'A'`)
* Not resetting frequency array for each test case

## Interview Relevance

* Demonstrates frequency counting techniques
* Reinforces character-to-index mapping
* Introduces simple deficit-based counting logic

## What This Problem Teaches

* Efficient counting with fixed alphabets
* Mapping characters to array indices
* Handling multiple test cases cleanly

## Key Takeaways

* Fixed-range categories allow constant-space solutions
* Frequency counting is a powerful technique
* Always compare required counts with existing counts

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It primarily focuses on frequency counting and simple arithmetic operations, making it suitable for beginners and early competitive programming practice.