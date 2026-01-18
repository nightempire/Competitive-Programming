# A_Boring_Apartments

## Platform

Codeforces

## Problem Link

[A. Boring Apartments](https://codeforces.com/problemset/problem/1433/A)

## Problem Statement

There is a strange apartment building where each apartment number consists of only **one repeated digit**.

Valid apartment numbers are of the form:

```
1, 2, 3, ..., 9
11, 22, 33, ..., 99
111, 222, ..., 999
1111, 2222, ..., 9999
```

You are given an apartment number as a string.
Your task is to determine the **position (order)** of this apartment number in the sequence when all such boring apartment numbers are listed in increasing order.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains a string `s` representing the apartment number.

## Output Format

For each test case, output a single integer — the position of the given apartment number in the boring apartments sequence.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ |s| ≤ 4`
* The string consists of the same digit repeated (`'1'` to `'9'`)

## Examples

### Example 1

Input

```
4
1
22
333
4444
```

Explanation

* `1`   → first boring apartment
* `22`  → belongs to digit `2`, length `2`
* `333` → belongs to digit `3`, length `3`
* `4444` → belongs to digit `4`, length `4`

Output

```
1
13
26
40
```

### Example 2

Input

```
3
9
11
555
```

Explanation

* `9`   → last single-digit boring apartment
* `11`  → first double-digit boring apartment
* `555` → digit `5`, length `3`

Output

```
9
11
23
```

## Approach

**Mathematical Counting with Fixed-Length Patterns**

The solution computes how many boring apartments come **before** the given one by counting:

* All boring apartments formed using smaller digits
* All boring apartments of the same digit but smaller lengths

## Intuition

For each digit from `1` to `9`, there are exactly **four** boring apartment numbers:

```
d
dd
ddd
dddd
```

So:

* Each digit contributes a fixed count of previous apartments
* The position depends only on:

  * The digit value
  * The length of the string

No actual number comparison is required.

## Algorithm Steps

* Read the number of test cases.
* For each apartment string:

  * Extract the digit from the first character.
  * Count how many apartments come from digits smaller than this digit.
  * Add the count of apartments formed by the same digit with smaller lengths.
* Output the final position.

## Visual Walkthrough

### Test Case 1

Input: `333`

```
Digits smaller than 3 → 1, 2
Each digit contributes → 10 apartments
Total so far → 2 × 10 = 20
```

Length-based addition:

```
Length = 3 → add 6
```

Final answer:

```
20 + 6 = 26
```

---

### Test Case 2

Input: `22`

```
Digits smaller than 2 → 1
Contribution → 10
```

Length-based addition:

```
Length = 2 → add 3
```

Final answer:

```
10 + 3 = 13
```

## Complexity Analysis

### Time Complexity

O(1) per test case

The computation involves constant-time arithmetic operations.

### Space Complexity

O(1)

No extra space proportional to input size is used.

## Solution Explanation

The solution avoids generating any apartment numbers explicitly.
It uses the predictable pattern of boring apartments:

* Each digit contributes a fixed block of apartments
* The length of the string determines the offset within that block

This makes the approach efficient, clean, and mathematically sound.

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

        // Apartment number as string
        string s;
        cin >> s;

        // Calculate contribution from digits smaller than s[0]
        int ans = s[0] != '1' ? (s[0] - '0' - 1) * 10 : 0;

        // Length of the apartment number
        int n = s.length();

        // Add contribution based on length
        if (n == 1) {
            ans += 1;
        } else if (n == 2) {
            ans += 3;
        } else if (n == 3) {
            ans += 6;
        } else {
            ans += 10;
        }

        // Output the final position
        cout << ans << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Apartment | Digit | Length | Calculated Position |
| --------- | ----- | ------ | ------------------- |
| 1         | 1     | 1      | 1                   |
| 22        | 2     | 2      | 13                  |
| 333       | 3     | 3      | 26                  |
| 4444      | 4     | 4      | 40                  |
| 9         | 9     | 1      | 81                  |

## Edge Cases to Consider

* Smallest apartment number (`1`)
* Largest apartment number (`9999`)
* Multiple test cases
* All valid lengths from `1` to `4`

## Common Test Cases

* Single-digit apartments
* Maximum-length apartments
* Sequential digits like `111`, `222`, `333`

## Common Mistakes to Avoid

* Treating the input as an integer instead of a string
* Forgetting fixed contributions per digit
* Using loops instead of constant-time calculations

## Interview Relevance

* Demonstrates pattern recognition
* Tests arithmetic reasoning
* Emphasizes optimization over brute force

## What This Problem Teaches

* How to leverage constraints for mathematical simplification
* Avoiding unnecessary computation
* Translating patterns into formulas

## Key Takeaways

* Fixed patterns enable O(1) solutions
* String length can encode positional information
* Clean logic often outperforms brute-force methods

## Problem Difficulty Analysis

This is an **Easy-level** problem.
While the logic is simple, it rewards observation and mathematical reasoning rather than iteration.