# C_Can_I_Square

## Platform

Codeforces

## Problem Link

[C. Can I Square?](https://codeforces.com/problemset/problem/1915/C)

## Problem Statement

You are given multiple test cases.
In each test case, you are given an integer `n` followed by `n` integers.

Your task is to determine whether the **sum of the given integers is a perfect square**.

For each test case:

* If the sum is a perfect square, print `"YES"`
* Otherwise, print `"NO"`

Each test case is independent.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`, the number of elements.
  * The second line contains `n` integers.

## Output Format

For each test case, print:

* `"YES"` if the sum of the elements is a perfect square
* `"NO"` otherwise

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 2 × 10^5` (across all test cases)
* `0 ≤ ai ≤ 10^9`
* The sum of `n` over all test cases does not exceed limits

## Examples

### Example 1

Input

```
3
3
1 2 6
2
2 2
1
0
```

Explanation

* Test case 1:

  * Sum = `1 + 2 + 6 = 9`
  * `9 = 3²` → perfect square → `YES`
* Test case 2:

  * Sum = `2 + 2 = 4`
  * `4 = 2²` → perfect square → `YES`
* Test case 3:

  * Sum = `0`
  * `0 = 0²` → perfect square → `YES`

Output

```
YES
YES
YES
```

### Example 2

Input

```
2
3
1 1 1
4
1 2 3 5
```

Explanation

* Test case 1:

  * Sum = `3`
  * Not a perfect square → `NO`
* Test case 2:

  * Sum = `11`
  * Not a perfect square → `NO`

Output

```
NO
NO
```

## Approach

**Mathematical validation using integer square root**

## Intuition

A number is a **perfect square** if and only if:

* Its integer square root, when squared, gives back the original number

Instead of checking all squares:

* Compute the sum
* Compute `floor(sqrt(sum))`
* Square it and compare with the original sum

This is efficient and avoids unnecessary computations.

## Algorithm Steps

* Read integer `t`
* For each test case:

  * Read integer `n`
  * Read `n` integers and compute their sum
  * Compute integer square root of the sum
  * If `(root × root == sum)`, print `"YES"`
  * Otherwise, print `"NO"`

## Visual Walkthrough

### Test Case 1

Input:

```
1 4 9
```

Sum:

```
1 + 4 + 9 = 14
```

Square root:

```
⌊√14⌋ = 3
3 × 3 = 9 ≠ 14
```

Result:

```
NO
```

---

### Test Case 2

Input:

```
4 5 7
```

Sum:

```
4 + 5 + 7 = 16
```

Square root:

```
⌊√16⌋ = 4
4 × 4 = 16
```

Result:

```
YES
```

---

### Test Case 3

Input:

```
0
```

Sum:

```
0
```

Square root:

```
0 × 0 = 0
```

Result:

```
YES
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each element is read once and added to the sum.
The square root computation is constant time.

### Space Complexity

**O(1)**

Only a few variables are used to store the sum and square root.
No additional memory proportional to input size is required.

## Solution Explanation

The solution accumulates the sum of the array elements using a 64-bit integer to avoid overflow.
It then computes the integer square root of the sum and verifies whether squaring it reproduces the original sum.

This direct mathematical check ensures correctness while remaining efficient for large inputs.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {

    // Fast input/output for large data
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Number of elements
        int n;
        cin >> n;

        // Variable to store the sum (64-bit to avoid overflow)
        long long sum = 0;

        // Read all elements and accumulate their sum
        for (int i = 0; i < n; i++) {
            long long num;
            cin >> num;
            sum += num;
        }

        // Compute integer square root of the sum
        long long sr = sqrt(sum);

        // Check if sum is a perfect square
        if (sr * sr == sum) {
            cout << "YES\n";
        } else {
            cout << "NO\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Input Numbers | Sum | Perfect Square | Output |
| --------- | ------------- | --- | -------------- | ------ |
| 1         | 1 2 6         | 9   | Yes            | YES    |
| 2         | 2 2           | 4   | Yes            | YES    |
| 3         | 1 1 1         | 3   | No             | NO     |
| 4         | 1 2 3 5       | 11  | No             | NO     |
| 5         | 0             | 0   | Yes            | YES    |

## Edge Cases to Consider

* Sum equals `0`
* Single-element arrays
* Very large values causing overflow if not using `long long`

## Common Test Cases

* All elements are zero
* Sum is just below a perfect square
* Sum is exactly a perfect square

## Common Mistakes to Avoid

* Using `int` instead of `long long` for the sum
* Comparing floating-point square roots directly
* Forgetting fast I/O for large inputs

## Interview Relevance

* Tests basic mathematical reasoning
* Evaluates integer overflow awareness
* Reinforces precision when using floating-point functions

## What This Problem Teaches

* Efficient perfect-square checking
* Safe handling of large sums
* Combining math with careful data types

## Key Takeaways

* Always guard against overflow
* Integer validation is safer than floating-point comparison
* Simple math checks can solve problems efficiently

## Problem Difficulty Analysis

This is an **Easy-to-Medium** level problem.
While the logic is simple, correct data type usage and mathematical validation are essential for correctness.