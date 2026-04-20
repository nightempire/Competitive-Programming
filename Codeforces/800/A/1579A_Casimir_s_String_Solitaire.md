## 1579A. Casimir's String Solitaire

## Platform

Codeforces

## Problem Link

[Casimir's String Solitaire](https://codeforces.com/problemset/problem/1579/A)

## Problem Statement

You are given a string `s` consisting only of characters `'A'`, `'B'`, and `'C'`.

You can repeatedly perform the following operation:

* Remove any occurrence of substring `"AB"` or `"BC"` from the string.

Determine whether it is possible to remove characters such that the string becomes **empty**.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains a string `s`.

## Output Format

* For each test case, print `"YES"` if it is possible to make the string empty, otherwise print `"NO"`.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ |s| ≤ 2 × 10^5`
* The total length of all strings does not exceed `2 × 10^5`
* String contains only `'A'`, `'B'`, `'C'`

## Examples

### Example 1

Input

```
3
ABBC
AABBCC
BAC
```

Explanation

* `ABBC` → remove `"AB"` → `BC` → remove `"BC"` → empty → YES
* `AABBCC` → operations possible → empty → YES
* `BAC` → no valid substring removal → NO

Output

```
YES
YES
NO
```

---

### Example 2

Input

```
2
ABC
BBB
```

Explanation

* `ABC` → remove `"AB"` → `C` → cannot proceed → NO
* `BBB` → no `"AB"` or `"BC"` → NO

Output

```
NO
NO
```

---

### Example 3

Input

```
1
ABBCBC
```

Explanation

```
ABBCBC → BCBC → BC → empty
```

Output

```
YES
```

## Approach

Greedy Observation (Frequency-Based Validation)

## Intuition

Each operation removes:

* `"AB"` → removes one `A` and one `B`
* `"BC"` → removes one `B` and one `C`

Thus:

* Every `A` must pair with a `B`
* Every `C` must also pair with a `B`

So the total number of `B`s must be exactly equal to:

```
count(A) + count(C)
```

This is the necessary and sufficient condition.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read string `s`
  * Count frequency of `'A'`, `'B'`, `'C'`
  * Check:

    * If `freq[B] == freq[A] + freq[C]`, print `"YES"`
    * Else, print `"NO"`

## Visual Walkthrough

### Case 1

```
s = "ABBC"
```

```
A = 1, B = 2, C = 1
B == A + C → 2 == 2 → YES
```

---

### Case 2

```
s = "BAC"
```

```
A = 1, B = 1, C = 1
B == A + C → 1 != 2 → NO
```

---

### Case 3

```
s = "AABBCC"
```

```
A = 2, B = 4, C = 2
B == A + C → 4 == 4 → YES
```

## Complexity Analysis

### Time Complexity

**O(n) per test case**

Each character is processed once.

### Space Complexity

**O(1)**

Only a fixed-size frequency array is used.

## Solution Explanation

The solution counts occurrences of each character and checks whether the number of `'B'` characters equals the sum of `'A'` and `'C'`. This works because every removal operation consumes exactly one `'B'` along with either an `'A'` or a `'C'`.

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

        // Frequency array for A, B, C
        int freq[3] = {0};

        // Count occurrences
        for(char ch : s) {
            freq[ch - 'A']++;
        }

        // Check condition:
        // number of B must equal number of A + C
        if(freq[1] == freq[0] + freq[2]) {
            cout << "YES\n";
        } else {
            cout << "NO\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| String | A | B | C | Condition (B = A + C) | Output |
| ------ | - | - | - | --------------------- | ------ |
| ABBC   | 1 | 2 | 1 | 2 = 2                 | YES    |
| BAC    | 1 | 1 | 1 | 1 ≠ 2                 | NO     |
| AABBCC | 2 | 4 | 2 | 4 = 4                 | YES    |
| BBB    | 0 | 3 | 0 | 3 ≠ 0                 | NO     |

## Edge Cases to Consider

* String with only one type of character
* Minimum length string (`|s| = 1`)
* All characters are balanced vs unbalanced

## Common Test Cases

* Equal distribution of A, B, C
* Only B characters
* No B characters
* Mixed random patterns

## Common Mistakes to Avoid

* Checking order instead of frequency
* Trying to simulate removals (unnecessary)
* Using incorrect condition (e.g., `>=` instead of `==`)

## Interview Relevance

* Tests ability to identify hidden invariants
* Focuses on greedy reasoning
* Avoids unnecessary simulation

## What This Problem Teaches

* Reducing operations to mathematical conditions
* Using frequency counting effectively
* Recognizing patterns in string manipulation

## Key Takeaways

* Always look for invariants in removal problems
* Simulation is not always required
* Frequency-based reasoning can simplify problems

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The key challenge is identifying the invariant condition (`B = A + C`), after which the implementation is straightforward.