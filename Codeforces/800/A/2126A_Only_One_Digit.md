# A_Only_One_Digit

## Platform

Codeforces

## Problem Link

[A. Only One Digit](https://codeforces.com/problemset/problem/2126/A)

## Problem Statement

You are given an integer `x`.

Your task is to determine the **smallest digit** present in the decimal representation of `x`.

For each test case, output that smallest digit.

---

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each of the next `t` lines contains a single integer `x`.

---

## Output Format

For each test case, print a single integer — the smallest digit in `x`.

---

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ x ≤ 10^18`

---

## Examples

### Example 1

Input

```
3
123
908
444
```

Explanation

* `123` → digits: {1, 2, 3} → smallest = 1
* `908` → digits: {9, 0, 8} → smallest = 0
* `444` → digits: {4, 4, 4} → smallest = 4

Output

```
1
0
4
```

---

### Example 2

Input

```
2
7
100000
```

Explanation

* `7` → smallest digit = 7
* `100000` → digits include 0 → smallest = 0

Output

```
7
0
```

---

## Approach (Algorithm Type)

**Digit Extraction using Modulo and Division (Greedy Minimum Tracking)**

---

## Intuition

To analyze digits of a number:

* The last digit can be obtained using `x % 10`.
* Remove the last digit using integer division `x /= 10`.

By repeating this process until `x` becomes zero, we can examine all digits and keep track of the minimum one.

Since we only need the smallest digit, we maintain a running minimum.

---

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read integer `x`.
  * Initialize `y = 9` (maximum possible digit).
  * While `x > 0`:

    * Extract last digit: `d = x % 10`.
    * Update `y = min(y, d)`.
    * Remove last digit: `x /= 10`.
  * Print `y`.

---

## Visual Walkthrough

### Test Case 1

Input:

```
x = 908
```

Step-by-step:

| x   | x % 10 | Current Min |
| --- | ------ | ----------- |
| 908 | 8      | 8           |
| 90  | 0      | 0           |
| 9   | 9      | 0           |

Final answer → **0**

---

### Test Case 2

Input:

```
x = 123
```

| x   | x % 10 | Current Min |
| --- | ------ | ----------- |
| 123 | 3      | 3           |
| 12  | 2      | 2           |
| 1   | 1      | 1           |

Final answer → **1**

---

### Test Case 3

Input:

```
x = 7
```

Single digit → minimum is **7**

---

## Complexity Analysis

### Time Complexity

For each test case:

* Each digit is processed once.
* Number of digits in `x` is at most 18 (since `x ≤ 10^18`).

Therefore:

* **O(d)** per test case, where `d` is number of digits.
* Overall → **O(t × d)**.
* Since `d ≤ 18`, effectively **O(t)**.

---

### Space Complexity

**O(1)**

* Only constant variables are used.
* No extra data structures required.

---

## Solution Explanation

The solution iteratively extracts digits from the number using modulo operation.

A variable `y` stores the smallest digit found so far. It is initialized to `9` because that is the largest possible digit.

During each iteration:

* The last digit is extracted.
* The minimum value is updated.
* The number is reduced.

Once all digits are processed, `y` holds the smallest digit.

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

        // Input number
        long long x;

        // Initialize minimum digit to 9
        int y = 9;

        cin >> x;

        // Process each digit of x
        while(x > 0) {

            // Extract last digit
            int digit = x % 10;

            // Update minimum digit
            y = min(y, digit);

            // Remove last digit
            x /= 10;
        }

        // Output the smallest digit
        cout << y << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| Input x | Digits     | Smallest Digit |
| ------- | ---------- | -------------- |
| 123     | 1, 2, 3    | 1              |
| 908     | 9, 0, 8    | 0              |
| 444     | 4, 4, 4    | 4              |
| 100000  | 1, 0, 0... | 0              |
| 7       | 7          | 7              |

---

## Edge Cases to Consider

* Single digit number
* Number containing zero
* Number where all digits are identical
* Maximum possible value (`10^18`)

---

## Common Test Cases

* Numbers with zero
* Increasing digits
* Decreasing digits
* Repeated digits

---

## Common Mistakes to Avoid

* Using `int` instead of `long long` for large inputs
* Forgetting to reinitialize minimum for each test case
* Incorrect loop termination condition

---

## Interview Relevance

* Tests digit manipulation skills
* Reinforces modulo and division techniques
* Common warm-up problem for number processing

---

## What This Problem Teaches

* Extracting digits using arithmetic operations
* Maintaining running minimum
* Efficient handling of multiple test cases

---

## Key Takeaways

* Modulo (`% 10`) extracts the last digit.
* Division (`/ 10`) removes the last digit.
* Always consider numeric limits in competitive programming.

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses purely on digit manipulation and basic iteration, making it suitable for beginners and early competitive programming practice.