# B_Ordinary_Numbers

## Platform

Codeforces

## Problem Link

[B. Ordinary Numbers](https://codeforces.com/problemset/problem/1520/B)

## Problem Statement

A positive integer is called **ordinary** if all of its digits are the same.

Examples of ordinary numbers:

```
1, 2, 3, ..., 9
11, 22, 33, ..., 99
111, 222, 333, ...
```

Given an integer `n`, determine how many ordinary numbers are **less than or equal to `n`**.

---

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each of the next `t` lines contains a single integer `n`.

---

## Output Format

For each test case, print the count of ordinary numbers less than or equal to `n`.

---

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 10^9`

---

## Examples

### Example 1

Input

```
3
1
9
33
```

Explanation

* `n = 1` → ordinary numbers: {1} → count = 1
* `n = 9` → ordinary numbers: {1..9} → count = 9
* `n = 33` → ordinary numbers:
  1–9 (9 numbers)
  11, 22, 33 (3 numbers)
  Total = 12

Output

```
1
9
12
```

---

### Example 2

Input

```
2
100
7
```

Explanation

For `100`:

* 1-digit → 9 numbers
* 2-digit → 11,22,...,99 → 9 numbers
* 3-digit → 111 (greater than 100, so none)

Total = 18

For `7`:

* 1 to 7 → 7 ordinary numbers

Output

```
18
7
```

---

## Approach (Algorithm Type)

**Digit Length Analysis with Mathematical Counting**

---

## Intuition

Ordinary numbers follow a strict pattern:

For each digit `d` (1 to 9), we can form:

```
d
dd
ddd
dddd
...
```

If `n` has:

* Length `len`
* First digit `first`

Then:

* All ordinary numbers with fewer digits than `len` are valid.
* For numbers with same digit length:

  * Count how many repeated-digit numbers are ≤ `n`.

This leads to a direct mathematical formula.

---

## Key Observation

For numbers with fewer digits:

```
9 × (len - 1)
```

Because:

* Each digit length contributes 9 ordinary numbers.
* Example:

  * 1-digit → 9
  * 2-digit → 9
  * 3-digit → 9
  * and so on.

For numbers with the same digit length:

* We can form `first` possible candidates.
* But if the constructed repeated-digit number is greater than `n`, subtract 1.

---

## Algorithm Steps

* Read `t`.
* For each test case:

  * Read `n`.
  * Convert `n` to string.
  * Compute:

    * `len = length of n`
    * `first = first digit`
  * Compute base answer:

    ```
    ans = 9 × (len - 1) + first
    ```
  * Construct number:

    ```
    x = number formed by repeating 'first' digit len times
    ```
  * If `x > n`, decrement `ans`.
  * Print `ans`.

---

## Visual Walkthrough

### Test Case 1

Input:

```
n = 33
```

Length = 2
First digit = 3

Base:

```
9 × (2 - 1) = 9
```

Add first digit:

```
9 + 3 = 12
```

Construct:

```
33
```

Since 33 ≤ 33 → valid.

Answer = **12**

---

### Test Case 2

Input:

```
n = 35
```

Length = 2
First digit = 3

Base:

```
9 × 1 + 3 = 12
```

Construct:

```
33
```

33 ≤ 35 → valid.

Answer = **12**

---

### Test Case 3

Input:

```
n = 32
```

Length = 2
First digit = 3

Base:

```
9 × 1 + 3 = 12
```

Construct:

```
33
```

33 > 32 → subtract 1

Final = **11**

---

## Complexity Analysis

### Time Complexity

For each test case:

* Converting to string → O(d)
* Constructing repeated number → O(d)

Where `d ≤ 10` (since `n ≤ 10^9`).

Overall:

```
O(t)
```

---

### Space Complexity

```
O(1)
```

Only a few variables are used.

---

## Solution Explanation

The solution avoids generating all ordinary numbers.

Instead, it uses a direct mathematical count:

* Count all smaller-length ordinary numbers.
* Add possible same-length candidates.
* Adjust if constructed number exceeds `n`.

This ensures:

* No brute force
* Constant time per test case
* Efficient even for large `t`

---

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

        int n;
        cin >> n;

        // Convert number to string to easily get length and first digit
        string s = to_string(n);

        // Length of number
        int len = s.length();

        // First digit of number
        int first = s[0] - '0';

        // Count all ordinary numbers with smaller digit lengths
        int ans = 9 * (len - 1) + first;

        // Construct repeated-digit number of same length
        int x = 0;
        for(int i = 0; i < len; i++) {
            x = x * 10 + first;
        }

        // If constructed number is greater than n,
        // subtract one from answer
        if(x > n) {
            ans--;
        }

        // Output result
        cout << ans << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| n   | len | Base Count | Adjustment | Final Answer |
| --- | --- | ---------- | ---------- | ------------ |
| 1   | 1   | 1          | 0          | 1            |
| 9   | 1   | 9          | 0          | 9            |
| 32  | 2   | 12         | -1         | 11           |
| 33  | 2   | 12         | 0          | 12           |
| 100 | 3   | 18         | -1         | 18           |

---

## Edge Cases to Consider

* Single digit numbers
* Exact ordinary numbers (like 11, 22, 333)
* Just below an ordinary number (like 32 before 33)
* Maximum constraint (`10^9`)

---

## Common Test Cases

* n = 1
* n = 10
* n = 99
* n = 100
* n = 111
* n = 1000000000

---

## Common Mistakes to Avoid

* Forgetting to subtract when constructed number exceeds `n`
* Incorrect calculation of base count
* Off-by-one errors

---

## Interview Relevance

* Demonstrates pattern recognition
* Uses mathematical counting instead of brute force
* Efficient number analysis technique

---

## What This Problem Teaches

* Counting by digit length
* Recognizing numeric patterns
* Avoiding unnecessary iteration

---

## Key Takeaways

* Many counting problems can be solved mathematically.
* Always analyze digit patterns before brute forcing.
* Length-based reasoning is powerful for number problems.

---

## Problem Difficulty Analysis

This is an **Easy to Lower-Medium** problem on Codeforces.

While conceptually simple, it requires recognizing the pattern and deriving the correct formula, making it slightly more analytical than basic iteration problems.