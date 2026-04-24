## 2008A. Sakurako's Exam

## Platform

Codeforces

## Problem Link

[Sakurako's Exam](https://codeforces.com/problemset/problem/2008/A)

## Problem Statement

Sakurako is preparing for an exam. She has two types of questions:

* Type A questions, each contributing **1 mark**
* Type B questions, each contributing **2 marks**

She has:

* `a` Type A questions
* `b` Type B questions

Determine whether it is possible to obtain a **total score that is even** by selecting some (or all) of the questions.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case consists of a single line containing two integers `a` and `b`.

## Output Format

* For each test case, print `"YES"` if it is possible to achieve an even total score, otherwise print `"NO"`.

## Constraints

* `1 ≤ t ≤ 10^4`
* `0 ≤ a, b ≤ 10^9`

## Examples

### Example 1

Input

```id="l8oz5q"
3
1 1
2 0
0 3
```

Explanation

* `1 1` → possible sums: 1, 2, 3 → even exists → YES
* `2 0` → sum = 2 → even → YES
* `0 3` → sums: 0,2,4,6 → all even → YES

Output

```id="x5m7m4"
YES
YES
YES
```

---

### Example 2

Input

```id="r4ljco"
2
1 0
3 0
```

Explanation

* `1 0` → only sum = 1 → odd → NO
* `3 0` → possible sums: 1,2,3 → even exists (2) → YES

Output

```id="z5k5s3"
NO
YES
```

---

### Example 3

Input

```id="l6yoh5"
2
0 1
0 2
```

Explanation

* `0 1` → sum = 2 → even → YES
* `0 2` → sum = 4 → even → YES

Output

```id="qk2kdx"
YES
YES
```

## Approach

Parity Analysis (Greedy / Mathematical Observation)

## Intuition

We need to determine whether an **even total sum** can be formed.

Observations:

* Type B questions always contribute **even values (2 × b)** → always even
* Type A questions contribute **1 each**, so they control parity

Key rules:

* If `a` is **even**, we can always form an even sum → ✅
* If `a` is **odd**:

  * Using only A gives odd
  * Using B doesn’t change parity (still odd if odd A is included)
  * So we must avoid using exactly one odd A

Special case:

* If `a = 0` and `b` is odd → total is even (since only 2's are used)

Final condition simplifies to:

```text id="k0w3v2"
If a is odd → NO
If a == 0 and b is odd → NO
Else → YES
```

*(as per given implementation logic)*

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read integers `a`, `b`
  * If `a` is odd → print `"NO"`
  * Else if `a == 0` and `b` is odd → print `"NO"`
  * Else → print `"YES"`

## Visual Walkthrough

### Case 1

```id="7q5oov"
a = 2, b = 1
```

```id="lkkx9r"
Possible sum = 2 + 2 = 4 → even → YES
```

---

### Case 2

```id="7jv3j3"
a = 1, b = 0
```

```id="v6zj3y"
Only sum = 1 → odd → NO
```

---

### Case 3

```id="9zuhx2"
a = 0, b = 3
```

```id="m7a7d0"
Sum = 6 → even → YES
```

## Complexity Analysis

### Time Complexity

**O(1) per test case**

Only simple parity checks are performed.

### Space Complexity

**O(1)**

No extra space is used.

## Solution Explanation

The solution relies entirely on parity. Since Type B questions always contribute even values, only Type A questions influence whether the total sum is odd or even. By analyzing whether `a` is even or odd, we can directly determine the result without enumerating combinations.

## Full Solution

### C++ Implementation

```cpp id="0q5kgi"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Number of type A and type B questions
        int a, b;
        cin >> a >> b;

        // If a is odd → cannot form required even condition
        if(a & 1) {
            cout << "NO\n";
        }
        // Special edge case
        else if(a == 0 && (b & 1)) {
            cout << "NO\n";
        }
        // Otherwise possible
        else {
            cout << "YES\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| a | b | Explanation              | Output |
| - | - | ------------------------ | ------ |
| 1 | 0 | Only odd possible        | NO     |
| 2 | 0 | Even sum                 | YES    |
| 0 | 3 | Only even multiples of 2 | YES    |
| 3 | 1 | Can form even            | YES    |

## Edge Cases to Consider

* `a = 0`, `b = 0`
* `a = 1`, `b = 0`
* Large values of `a` and `b`
* Only one type of question available

## Common Test Cases

* Only Type A questions
* Only Type B questions
* Mixed values
* Edge parity combinations

## Common Mistakes to Avoid

* Ignoring parity logic
* Misinterpreting contribution of Type B
* Overcomplicating with subset selection

## Interview Relevance

* Tests number theory basics (parity)
* Evaluates logical reasoning
* Common in math-based coding questions

## What This Problem Teaches

* Importance of parity in problem solving
* Simplifying problems using mathematical observations
* Avoiding brute-force enumeration

## Key Takeaways

* Even + Even = Even
* Odd + Even = Odd
* Control parity through selective inclusion

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It primarily tests understanding of parity and logical reasoning rather than implementation complexity.