# B_Good_Kid

## Platform

Codeforces

## Problem Link

[B. Good Kid](https://codeforces.com/problemset/problem/1873/B)

## Problem Statement

You are given an array of integers for each test case.
You are allowed to **increase exactly one element by 1**.

After performing this operation, compute the **maximum possible product** of all elements in the array.

Your task is to output this maximum product for each test case.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`, the size of the array.
  * The second line contains `n` integers representing the array elements.

## Output Format

For each test case, print a single integer — the maximum possible product after increasing exactly one element by `1`.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 50`
* `0 ≤ a[i] ≤ 9`

## Examples

### Example 1

Input

```
3
3
1 2 3
3
0 0 1
4
2 2 2 2
```

Explanation

* Test case 1:

  * Best choice is to increase `1 → 2`
  * Product becomes `2 × 2 × 3 = 12`
* Test case 2:

  * Increase one `0 → 1`
  * Product becomes `1 × 0 × 1 = 0`
* Test case 3:

  * Increase any `2 → 3`
  * Product becomes `3 × 2 × 2 × 2 = 24`

Output

```
12
0
24
```

## Approach

**Greedy Optimization Using Minimum Element Adjustment**

The solution maximizes the product by increasing the **smallest non-zero element** whenever possible, while carefully handling zeros.

## Intuition

To maximize a product:

* Increasing a **smaller value** gives a larger multiplicative benefit than increasing a larger one.
* Zeros are special:

  * Increasing one zero removes a multiplication by zero
  * Remaining zeros still force the product to be zero

Thus:

* If zeros exist, increase exactly one zero
* Otherwise, increase the smallest element

## Algorithm Steps

* Read number of test cases.
* For each test case:

  * Read array size and elements
  * Track:

    * Product of elements
    * Minimum element
    * Presence of zero
  * Skip multiplying exactly one zero
  * If the minimum element is non-zero:

    * Replace it with `(min + 1)` in the product
* Output the final product

## Visual Walkthrough

### Test Case 1

Input: `1 2 3`

```
Initial product = 6
Minimum element = 1
Increase 1 → 2
New product = (6 / 1) × 2 = 12
```

---

### Test Case 2

Input: `0 0 1`

```
Increase one 0 → 1
Remaining 0 keeps product = 0
```

Final answer:

```
0
```

---

### Test Case 3

Input: `2 2 2 2`

```
Minimum element = 2
Increase one 2 → 3
New product = (16 / 2) × 3 = 24
```

## Complexity Analysis

### Time Complexity

O(n) per test case

Each element is processed once.

### Space Complexity

O(1)

Only constant extra variables are used.

## Solution Explanation

The solution calculates the product of all elements while tracking the smallest element and detecting zeros.
If zeros exist, increasing one zero is optimal but may still result in a zero product due to remaining zeros.
If no zeros exist, increasing the smallest value yields the maximum possible product.

This greedy approach ensures optimal results without unnecessary recalculation.

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

        int n;
        cin >> n;

        int p = 1;          // Product of elements
        int mini = 9;       // Minimum element
        bool zeroFlag = false;

        // Read array elements
        for (int i = 0; i < n; i++) {
            int num;
            cin >> num;

            // Track minimum value
            if (num < mini)
                mini = num;

            // Skip multiplying exactly one zero
            if (!num && !zeroFlag) {
                zeroFlag = true;
                continue;
            }

            // Multiply non-zero or remaining elements
            p *= num;
        }

        // If minimum is non-zero, replace it with (min + 1)
        if (mini != 0)
            p = (p / mini) * (mini + 1);

        // Output result
        cout << p << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input Array | Zero Present | Min Element | Output |
| ----------- | ------------ | ----------- | ------ |
| 1 2 3       | No           | 1           | 12     |
| 0 0 1       | Yes          | 0           | 0      |
| 2 2 2 2     | No           | 2           | 24     |
| 0 5         | Yes          | 0           | 5      |

## Edge Cases to Consider

* All elements are zero
* Exactly one element in the array
* Array with both zero and non-zero values
* Maximum array size

## Common Test Cases

* Arrays with one zero
* Arrays with no zeros
* Arrays with repeated minimum values

## Common Mistakes to Avoid

* Increasing a non-minimum element
* Forgetting zero handling
* Recomputing product inefficiently

## Interview Relevance

* Tests greedy decision-making
* Reinforces product optimization strategies
* Common problem in array manipulation rounds

## What This Problem Teaches

* How local greedy choices affect global optimization
* Special-case handling (zeros)
* Efficient product manipulation

## Key Takeaways

* Increasing the smallest value maximizes product growth
* Zeros must be handled carefully in multiplicative problems
* Simple logic can outperform brute force approaches

## Problem Difficulty Analysis

This is an **Easy-to-Medium level** problem.
While the idea is simple, correct handling of zeros and edge cases requires careful reasoning.