# A_Extremely_Round

## Platform

Codeforces

## Problem Link

[A. Extremely Round](https://codeforces.com/problemset/problem/1766/A)

## Problem Statement

A number is called **extremely round** if it has **exactly one non-zero digit**.

Examples of extremely round numbers:

```
1, 2, 3, ..., 9, 10, 20, 30, ..., 100, 200, ...
```

Non-examples:

```
11, 101, 123
```

You are given an integer `n`.

Your task is to count how many extremely round numbers are **less than or equal to `n`**.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each test case contains a single integer:

```text
n
```

## Output Format

For each test case, print a single integer — the count of extremely round numbers ≤ `n`.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 10^9`

## Examples

### Example 1

Input

```
3
1
9
10
```

Explanation

Case 1:

```
n = 1
→ [1]
```

Count = `1`

---

Case 2:

```
n = 9
→ [1,2,3,4,5,6,7,8,9]
```

Count = `9`

---

Case 3:

```
n = 10
→ [1,2,...,9,10]
```

Count = `10`

Output

```
1
9
10
```

---

### Example 2

Input

```
2
55
100
```

Explanation

Case 1:

```
1–9 → 9 numbers
10,20,30,40,50 → 5 numbers
```

Total = `14`

---

Case 2:

```
1–9 → 9
10–90 → 9
100 → 1
```

Total = `19`

Output

```
14
19
```

## Approach

Digit Counting with Leading Digit Extraction

## Intuition

Extremely round numbers follow the pattern:

```
d × 10^k   where d ∈ [1..9]
```

So for each number of digits:

* 1-digit → 9 numbers
* 2-digit → 9 numbers
* 3-digit → 9 numbers
* ...

Thus:

```
For (digit - 1) full lengths → 9 × (digit - 1)
```

For the current digit length:

* Count how many leading digits are possible

This is:

```
n / (10^(digit - 1))
```

## Algorithm Steps

* Read integer `t`
* For each test case:

  * Read `n`
  * Compute number of digits:

```
digit = floor(log10(n)) + 1
```

* Compute:

```
result = 9 × (digit - 1) + (n / 10^(digit - 1))
```

* Print result

## Visual Walkthrough

### Test Case 1

```
n = 55
```

Digits:

```
2 digits
```

Count:

```
1-digit → 9
2-digit → leading digits = 55 / 10 = 5
```

Total:

```
9 + 5 = 14
```

---

### Test Case 2

```
n = 347
```

Digits:

```
3 digits
```

Count:

```
1-digit → 9
2-digit → 9
3-digit → 347 / 100 = 3
```

Total:

```
9 + 9 + 3 = 21
```

---

### Test Case 3

```
n = 1000
```

Digits:

```
4 digits
```

Count:

```
1-digit → 9
2-digit → 9
3-digit → 9
4-digit → 1000 / 1000 = 1
```

Total:

```
27 + 1 = 28
```

## Complexity Analysis

### Time Complexity

```
O(1) per test case
```

Only mathematical operations are performed.

### Space Complexity

```
O(1)
```

No extra space required.

## Solution Explanation

The solution avoids iterating through numbers.

Instead, it:

* Counts all extremely round numbers with fewer digits
* Adds the count of valid numbers with the same number of digits as `n`

The formula:

```
9 × (digit - 1)
```

counts all smaller digit lengths.

The term:

```
n / 10^(digit - 1)
```

counts valid numbers in the current digit range.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
#include<cmath>
using namespace std;

int main() {

    int t;
    cin >> t;

    while(t--) {

        int n;
        cin >> n;

        // Number of digits in n
        int digit = floor(log10(n)) + 1;

        // Count extremely round numbers
        int result = 9 * (digit - 1) + n / (int)pow(10, digit - 1);

        cout << result << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n   | Digits | Count |
| --- | ------ | ----- |
| 1   | 1      | 1     |
| 9   | 1      | 9     |
| 10  | 2      | 10    |
| 55  | 2      | 14    |
| 100 | 3      | 19    |
| 347 | 3      | 21    |

## Edge Cases to Consider

* `n < 10`
* Powers of 10 (10, 100, 1000)
* Large `n` near `10^9`

## Common Test Cases

```
1
9
10
99
100
999
1000
```

## Common Mistakes to Avoid

* Incorrect digit calculation
* Floating-point precision issues with `pow`
* Off-by-one errors in counting

## Interview Relevance

* Demonstrates pattern recognition
* Shows mathematical optimization
* Avoids brute-force counting

## What This Problem Teaches

* Digit-based counting techniques
* Efficient use of logarithms
* Pattern-based problem solving

## Key Takeaways

* Extremely round numbers follow a simple structure
* Count by digit groups instead of iterating
* Mathematical insights reduce complexity

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The key is recognizing the pattern of extremely round numbers and converting it into a direct mathematical formula for efficient computation.