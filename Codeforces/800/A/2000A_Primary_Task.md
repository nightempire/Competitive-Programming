## Platform

Codeforces

## Problem Link

[A. Primary Task](https://codeforces.com/problemset/problem/2000/A)

---

## Problem Statement

You are given a string `s` consisting of digits.

Determine whether the string represents a **valid number according to the following conditions**:

* The string must start with `"10"`
* The number must be **strictly greater than 10**
* The number must **not contain leading zeros after "10" in a way that makes it invalid**

Print `"YES"` if the string satisfies all conditions, otherwise print `"NO"`.

---

## Input Format

* The first line contains an integer `t` — number of test cases.
* Each test case consists of a string `s`.

---

## Output Format

For each test case:

* Print `"YES"` if valid
* Otherwise print `"NO"`

---

## Constraints

* `1 ≤ t ≤ 1000`
* `3 ≤ |s| ≤ 100`
* `s` consists only of digits (`0–9`)

---

## Examples

### Example 1

Input

```id="p7wq1m"
4
101
100
102
109
```

Explanation

* `101` → starts with "10" and > 10 → valid
* `100` → starts with "10" but next digit is 0 → invalid
* `102` → valid
* `109` → valid

Output

```id="v2k3mj"
YES
NO
YES
YES
```

---

### Example 2

Input

```id="pnnrbf"
3
10
110
1010
```

Explanation

* `10` → not strictly greater → invalid
* `110` → does not start with "10" → invalid
* `1010` → valid

Output

```id="mv8dr2"
NO
NO
YES
```

---

### Example 3

Input

```id="ny2h3t"
2
103
1000
```

Explanation

* `103` → valid
* `1000` → invalid due to leading zero pattern after "10"

Output

```id="4xf3ld"
YES
NO
```

---

## Approach

Pattern checking using string conditions

---

## Intuition

The problem reduces to validating a number based on:

* Fixed prefix `"10"`
* Value must be strictly greater than `10`
* The third character determines validity:

  * If it is `'0'` → invalid
  * If it is `'1'`, the string must be longer than 3 (to ensure > 10)
  * If it is `'2'` to `'9'` → always valid

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read string `s`
  * Check:

    * First character is `'1'`
    * Second character is `'0'`
    * Third character:

      * If `'0'` → invalid
      * If `'1'` → valid only if length > 3
      * If `'2'–'9'` → valid
  * Print result accordingly

---

## Visual Walkthrough

### Case 1: `"101"`

```id="u9x2t0"
Prefix = "10"
Third char = '1'
Length = 3 → not > 3 → invalid
```

---

### Case 2: `"102"`

```id="b9r5pd"
Prefix = "10"
Third char = '2' → valid
```

---

### Case 3: `"100"`

```id="e1d6az"
Prefix = "10"
Third char = '0' → invalid
```

---

## Complexity Analysis

### Time Complexity

O(n) per test case

* Reading and checking string characters

---

### Space Complexity

O(1)

* No extra space used

---

## Solution Explanation

The solution checks for a strict structural pattern in the string:

* It first validates the prefix `"10"`
* Then evaluates the third character to determine whether the number is strictly greater than 10 and not malformed

This avoids integer conversion and ensures efficient string-based validation.

---

## Full Solution

### C++ Implementation

```cpp id="9h1l0y"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while(t--) {

        // Input string
        string s;
        cin >> s;

        // Length of string
        int n = s.length();

        // Check required conditions:
        // 1. Starts with "10"
        // 2. Third character logic for validity
        if(s[0] == '1' && s[1] == '0' &&
           (
               // Case 1: Third character is '1' but length must be > 3
               (s[2] == '1' && n > 3)

               ||

               // Case 2: Third character is between '2' and '9'
               (s[2] >= '2')
           )
        ) {

            cout << "YES\n";

        } else {

            cout << "NO\n";
        }
    }

    return 0;
}
```

---

## Test Cases Analysis

| String | Starts with "10" | Third Char | Length | Output |
| ------ | ---------------- | ---------- | ------ | ------ |
| 101    | Yes              | 1          | 3      | NO     |
| 102    | Yes              | 2          | 3      | YES    |
| 100    | Yes              | 0          | 3      | NO     |
| 1010   | Yes              | 1          | 4      | YES    |
| 110    | No               | —          | —      | NO     |

---

## Edge Cases to Consider

* Minimum length strings (`|s| = 3`)
* Third character = `'0'`
* Strings starting with other prefixes
* Large length strings

---

## Common Test Cases

* `101` → NO
* `102` → YES
* `100` → NO
* `1010` → YES

---

## Common Mistakes to Avoid

* Ignoring prefix validation `"10"`
* Allowing `"100"` as valid
* Not checking length when third char is `'1'`

---

## Interview Relevance

* String pattern validation
* Edge case handling
* Conditional logic optimization

---

## What This Problem Teaches

* Efficient string-based checks
* Avoiding unnecessary conversions
* Breaking conditions into structured rules

---

## Key Takeaways

* Pattern-based problems can often be solved without parsing numbers
* Always validate prefix conditions first
* Edge cases (like leading zeros) are critical

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* String manipulation
* Conditional checks
* Edge case handling