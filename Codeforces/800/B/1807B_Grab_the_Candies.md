# B_Grab_the_Candies

## Platform

Codeforces

## Problem Link

[B. Grab the Candies](https://codeforces.com/problemset/problem/1807/B)

---

## Problem Statement

You are given an array of integers representing candies.

You are allowed to collect:

* All candies with **even values**
* All candies with **odd values**

Your goal is to determine whether the **sum of even candies is strictly greater than the sum of odd candies**.

If it is, print:

```
YES
```

Otherwise, print:

```
NO
```

---

## Input Format

* The first line contains an integer `t` — number of test cases.
* For each test case:

  * An integer `n` — number of candies.
  * A line containing `n` integers.

---

## Output Format

For each test case, print `YES` if the sum of even numbers is strictly greater than the sum of odd numbers; otherwise print `NO`.

---

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 100`
* `1 ≤ ai ≤ 100`

---

## Examples

### Example 1

Input

```
3
3
2 4 6
4
1 3 5 7
5
1 2 3 4 5
```

Explanation

Test Case 1
Even sum = 2 + 4 + 6 = 12
Odd sum = 0
→ 12 > 0 → YES

Test Case 2
Even sum = 0
Odd sum = 1 + 3 + 5 + 7 = 16
→ 0 > 16 → NO

Test Case 3
Even sum = 2 + 4 = 6
Odd sum = 1 + 3 + 5 = 9
→ 6 > 9 → NO

Output

```
YES
NO
NO
```

---

## Approach (Algorithm Type)

**Single Pass Iteration with Conditional Aggregation**

---

## Intuition

We need to compare:

```
Sum of even numbers  >  Sum of odd numbers
```

Instead of storing two separate sums, we can maintain a single variable `diff`:

* Add even numbers to `diff`
* Subtract odd numbers from `diff`

At the end:

* If `diff > 0` → even sum is greater.
* Otherwise → not greater.

This avoids maintaining two separate accumulators.

---

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read integer `n`.
  * Initialize `diff = 0`.
  * For each number:

    * If number is even:

      * `diff += number`
    * Else:

      * `diff -= number`
  * If `diff > 0`:

    * Print `YES`
  * Else:

    * Print `NO`

---

## Visual Walkthrough

### Test Case 1

Input:

```
2 4 6
```

Process:

| Number | Type | diff |
| ------ | ---- | ---- |
| 2      | Even | 2    |
| 4      | Even | 6    |
| 6      | Even | 12   |

Final:
`diff = 12` → YES

---

### Test Case 2

Input:

```
1 3 5 7
```

Process:

| Number | Type | diff |
| ------ | ---- | ---- |
| 1      | Odd  | -1   |
| 3      | Odd  | -4   |
| 5      | Odd  | -9   |
| 7      | Odd  | -16  |

Final:
`diff = -16` → NO

---

### Test Case 3

Input:

```
1 2 3 4 5
```

Process:

| Number | Type | diff |
| ------ | ---- | ---- |
| 1      | Odd  | -1   |
| 2      | Even | 1    |
| 3      | Odd  | -2   |
| 4      | Even | 2    |
| 5      | Odd  | -3   |

Final:
`diff = -3` → NO

---

## Complexity Analysis

### Time Complexity

For each test case:

* Traverse array once → O(n)

Overall:

```
O(total elements across all test cases)
```

Given constraints, this is efficient.

---

### Space Complexity

```
O(1)
```

Only one integer variable is used.

---

## Solution Explanation

The solution leverages parity checking:

```
num & 1
```

* If result is 1 → odd
* If result is 0 → even

By accumulating even values positively and odd values negatively into a single variable `diff`, we reduce logic complexity.

Final decision depends solely on whether `diff` is positive.

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

        // diff will store:
        // (sum of even numbers) - (sum of odd numbers)
        int diff = 0;

        cin >> n;

        // Process each candy
        for(int i = 0; i < n; i++) {

            int num;
            cin >> num;

            // If number is odd
            if(num & 1) {

                // Subtract odd numbers
                diff -= num;
            }
            else {

                // Add even numbers
                diff += num;
            }
        }

        // If even sum is strictly greater
        cout << (diff > 0 ? "YES\n" : "NO\n");
    }

    return 0;
}
```

---

## Test Cases Analysis

| Array     | Even Sum | Odd Sum | Output |
| --------- | -------- | ------- | ------ |
| 2 4 6     | 12       | 0       | YES    |
| 1 3 5 7   | 0        | 16      | NO     |
| 1 2 3 4 5 | 6        | 9       | NO     |
| 8 2 1     | 10       | 1       | YES    |
| 1         | 0        | 1       | NO     |

---

## Edge Cases to Consider

* All numbers are even
* All numbers are odd
* Single element array
* Equal even and odd sums

---

## Common Test Cases

* Mixed parity
* Large number of small elements
* Balanced sums
* Minimum constraints

---

## Common Mistakes to Avoid

* Using `>=` instead of `>`
* Forgetting to reset `diff` for each test case
* Incorrect parity check

---

## Interview Relevance

* Tests understanding of parity logic
* Reinforces single-pass aggregation
* Demonstrates clean condition-based accumulation

---

## What This Problem Teaches

* Efficient iteration patterns
* Using bitwise operations for parity checking
* Comparing grouped sums

---

## Key Takeaways

* Parity check using `num & 1` is efficient.
* Problems can often be simplified by tracking differences.
* Single-pass solutions improve clarity and performance.

---

## Problem Difficulty Analysis

This is an **Easy-level** Codeforces problem.

It focuses on conditional aggregation and parity checking, making it ideal for beginners and early contest practice.