# A. Polycarp and Coins

## Platform

Codeforces

## Problem Link

[A. Polycarp and Coins](https://codeforces.com/problemset/problem/1551/A)

## Problem Statement

Polycarp has `n` coins.
He wants to distribute these coins into **two piles** such that:

* One pile contains coins of value `1`
* The other pile contains coins of value `2`
* The **total value** of coins in both piles is exactly `n`
* The **difference between the number of coins** in the two piles is minimized

For each test case, determine how many coins of value `1` and value `2` Polycarp should take.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains a single integer `n`.

## Output Format

For each test case, print two integers:

* Number of coins with value `1`
* Number of coins with value `2`

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 10^9`

## Examples

### Example 1

Input

```
3
1
2
3
```

Explanation

* `n = 1` → `1 = 1`
* `n = 2` → `2 = 2`
* `n = 3` → `1 + 2 = 3`

Output

```
1 0
0 1
1 1
```

### Example 2

Input

```
2
4
5
```

Explanation

* `n = 4` → `2 + 2`
* `n = 5` → `3 + 2`

Output

```
2 1
2 1
```

## Approach

Greedy distribution based on division by 3.

## Intuition

To minimize the difference between the number of coins in both piles:

* Split `n` as evenly as possible between values `1` and `2`
* Since `1 + 2 = 3`, dividing `n` by `3` gives a balanced base distribution
* The remainder (`n % 3`) determines which pile needs an extra coin

This guarantees both correctness and optimal balance.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Compute `c1 = n / 3` and `c2 = n / 3`
  * If `n % 3 == 1`, increment `c1`
  * If `n % 3 == 2`, increment `c2`
  * Output `c1` and `c2`

## Visual Walkthrough

### Test Case 1

Input:

```
n = 4
```

Computation:

```
4 / 3 = 1
remainder = 1
```

Adjustment:

```
c1 = 2, c2 = 1
```

Result:

```
2*1 + 1*2 = 4
```

---

### Test Case 2

Input:

```
n = 5
```

Computation:

```
5 / 3 = 1
remainder = 2
```

Adjustment:

```
c1 = 1, c2 = 2
```

Result:

```
1*1 + 2*2 = 5
```

---

### Test Case 3

Input:

```
n = 6
```

Computation:

```
6 / 3 = 2
remainder = 0
```

Result:

```
c1 = 2, c2 = 2
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case is processed using constant-time arithmetic operations.

### Space Complexity

O(1)

Only a few integer variables are used.

## Solution Explanation

The solution distributes coins as evenly as possible using division by `3`.
Any remainder is handled by assigning an extra coin to the pile that best maintains balance.

This greedy strategy ensures the minimum possible difference in the number of coins.

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

        // Total value of coins
        int n;
        cin >> n;

        // Base distribution
        int c1 = n / 3;
        int c2 = n / 3;

        // Handle remainder
        if (n % 3 == 1)
            c1++;
        else if (n % 3 == 2)
            c2++;

        // Output the result
        cout << c1 << " " << c2 << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n | Output (c1, c2) | Reason              |
| - | --------------- | ------------------- |
| 1 | 1 0             | Only one coin       |
| 2 | 0 1             | Single value-2 coin |
| 3 | 1 1             | Balanced            |
| 4 | 2 1             | Remainder 1         |
| 5 | 1 2             | Remainder 2         |

## Edge Cases to Consider

* `n = 1`
* `n = 2`
* Large values of `n`

## Common Test Cases

* Multiples of 3
* Values with remainder 1
* Values with remainder 2

## Common Mistakes to Avoid

* Incorrect handling of `n % 3`
* Swapping the increments for remainder cases
* Overcomplicating the logic

## Interview Relevance

* Demonstrates greedy reasoning
* Tests modular arithmetic understanding
* Common logic-based distribution problem

## What This Problem Teaches

* Using division and modulo effectively
* Designing balanced distributions
* Writing concise and correct logic

## Key Takeaways

* Greedy strategies often simplify problems
* Modulo arithmetic is powerful for case handling
* Balance constraints guide solution design

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on arithmetic reasoning and clean implementation rather than advanced algorithms.