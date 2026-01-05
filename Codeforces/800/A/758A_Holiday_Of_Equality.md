# A_Holiday_Of_Equality

## Platform

Codeforces

## Problem Link

[A. Holiday Of Equality](https://codeforces.com/problemset/problem/758/A)

## Problem Statement

A group of `n` citizens is preparing for a holiday.
Each citizen has a certain amount of money.

To celebrate equality, the government wants **all citizens to have the same amount of money**.
They are allowed to **give extra money**, but **cannot take money away** from anyone.

Your task is to calculate the **minimum total amount of money** that must be distributed so that everyone ends up with an equal amount.

## Input Format

* The first line contains an integer `n`, the number of citizens.
* The second line contains `n` integers representing the amount of money each citizen currently has.

## Output Format

Print a single integer — the minimum total money that must be added to achieve equality.

## Constraints

* `1 ≤ n ≤ 100`
* `0 ≤ money[i] ≤ 100`
* Money can only be added, not removed

## Examples

### Example 1

Input

```
4
1 2 3 4
```

Explanation

* Maximum money among citizens is `4`
* Required additions:

  * `4 - 1 = 3`
  * `4 - 2 = 2`
  * `4 - 3 = 1`
  * `4 - 4 = 0`
* Total added money = `3 + 2 + 1 + 0 = 6`

Output

```
6
```

### Example 2

Input

```
3
5 5 5
```

Explanation

* All citizens already have equal money
* No money needs to be added

Output

```
0
```

## Approach (Algorithm Name / Type)

**Maximum Normalization via Linear Scan**

This approach raises all values to the maximum value found in the array using additive differences.

## Intuition

Since money cannot be taken away, the **final equal value must be the maximum** amount already present.

To make everyone equal:

* Find the maximum value.
* Add enough money to each citizen so their amount matches this maximum.

The sum of these differences gives the minimum required money.

## Algorithm Steps

* Read the number of citizens `n`.
* Read all money values and determine the maximum value.
* Initialize a sum variable.
* For each citizen:

  * Add `(maximum − current money)` to the sum.
* Output the final sum.

## Visual Walkthrough

### Test Case 1

Input:

```
1 2 3 4
```

Maximum value:

```
4
```

Money needed:

```
Citizen 1 → 4 - 1 = 3
Citizen 2 → 4 - 2 = 2
Citizen 3 → 4 - 3 = 1
Citizen 4 → 4 - 4 = 0
```

Total:

```
3 + 2 + 1 + 0 = 6
```

---

### Test Case 2

Input:

```
5 5 5
```

Maximum value:

```
5
```

Money needed:

```
0 + 0 + 0 = 0
```

---

### Test Case 3

Input:

```
0 2 2
```

Maximum value:

```
2
```

Money needed:

```
2 + 0 + 0 = 2
```

## Complexity Analysis

### Time Complexity

**O(n)**

The array is traversed twice:

* Once to find the maximum value
* Once to compute the required sum

Both operations are linear.

### Space Complexity

**O(1)**

Only a few integer variables are used.
No additional data structures are required beyond the input array.

## Solution Explanation

The solution works by first identifying the highest amount of money among all citizens. Since reductions are not allowed, this value becomes the target for everyone.

By summing the differences between the maximum value and each individual value, the solution computes the exact minimum amount of money that must be distributed to achieve equality.

This approach is efficient, simple, and directly reflects the problem constraints.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of citizens
    int n;
    cin >> n;

    // Array to store money of each citizen
    int nums[n];

    // Variable to track the maximum money value
    int maxi = 0;

    // Read money values and determine the maximum
    for (int i = 0; i < n; i++) {
        cin >> nums[i];

        // Update maximum if current value is greater
        if (nums[i] > maxi) {
            maxi = nums[i];
        }
    }

    // Variable to store total money required
    int totalMoney = 0;

    // Calculate how much money needs to be added
    for (int money : nums) {

        // Difference between maximum and current value
        totalMoney += maxi - money;
    }

    // Output the result
    cout << totalMoney;

    return 0;
}
```

## Test Cases Analysis

| Input      | Maximum | Total Added Money | Output |
| ---------- | ------- | ----------------- | ------ |
| `1 2 3 4`  | 4       | 6                 | 6      |
| `5 5 5`    | 5       | 0                 | 0      |
| `0 2 2`    | 2       | 2                 | 2      |
| `100 0 50` | 100     | 150               | 150    |

## Edge Cases to Consider

* All citizens already have equal money
* Only one citizen (`n = 1`)
* Some citizens have zero money

## Common Test Cases

* Mixed small and large values
* All identical values
* One significantly larger value than others

## Common Mistakes to Avoid

* Choosing the average instead of the maximum
* Forgetting that money cannot be taken away
* Incorrectly summing differences

## Interview Relevance

* Tests understanding of greedy normalization strategies
* Evaluates array traversal and aggregation skills
* Common introductory problem for optimization reasoning

## What This Problem Teaches

* How constraints influence algorithm design
* Efficient use of maximum values
* Translating real-world rules into computational logic

## Key Takeaways

* When reduction is not allowed, normalize to the maximum
* Linear scans are often sufficient for optimization problems
* Clear problem interpretation leads to simple solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It emphasizes logical reasoning and basic array manipulation rather than advanced algorithms, making it suitable for beginners and interview warm-up sessions.