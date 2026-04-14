## Platform

Codeforces

## Problem Link

[A. Phoenix and Balance](https://codeforces.com/problemset/problem/1348/A)

---

## Problem Statement

You are given an integer `n` (even).

You have `n` coins with weights:

```text
2¹, 2², 2³, ..., 2ⁿ
```

Your task is to divide these coins into **two groups of equal size (`n/2`)** such that:

* The **absolute difference** between the sums of the two groups is **maximized**

Output this maximum difference.

---

## Input Format

* The first line contains an integer `t` — number of test cases
* For each test case:

  * A single integer `n`

---

## Output Format

For each test case:

* Print the maximum possible difference

---

## Constraints

* `1 ≤ t ≤ 100`
* `2 ≤ n ≤ 30`
* `n` is even

---

## Examples

### Example 1

Input

```id="p7x3qk"
2
2
4
```

Explanation

* Case 1:

  * Coins: `[2, 4]`
  * Split: `{4}` and `{2}` → difference = 2

* Case 2:

  * Coins: `[2,4,8,16]`
  * Best split:

    * Group1: `{16, 2}`
    * Group2: `{4, 8}`
  * Difference = (16+2) - (4+8) = 6

Output

```id="k3m9vt"
2
6
```

---

### Example 2

Input

```id="z8m4xp"
1
6
```

Explanation

* Coins: `[2,4,8,16,32,64]`
* Optimal split:

  * Group1: `{64, 2, 4}`
  * Group2: `{8, 16, 32}`
* Difference = (64+2+4) - (8+16+32) = 14

Output

```id="t2k5rv"
14
```

---

### Example 3

Input

```id="m5p8xz"
1
8
```

Output

```id="y9k2qs"
30
```

---

## Approach

Greedy with power distribution

---

## Intuition

To maximize the difference:

* Put the **largest coin (`2ⁿ`)** in one group
* Add the **smallest `(n/2 - 1)` coins** to that same group
* Put the remaining **middle coins** in the other group

---

### Why this works?

* Largest coin dominates the sum
* Small coins minimally affect balance
* Middle coins grouped together reduce their impact

---

## Algorithm Steps

* Read `t`
* For each test case:

  * Read `n`
  * Initialize:

    * `sum1 = 2ⁿ`
  * Add smallest coins to `sum1`:

    ```
    for i = 1 to n/2 - 1:
        sum1 += 2^i
    ```
  * Add remaining coins to `sum2`:

    ```
    for i = n/2 to n-1:
        sum2 += 2^i
    ```
  * Print `|sum1 - sum2|`

---

## Visual Walkthrough

### Case 1: `n = 4`

```text id="s4k8zp"
Coins: 2, 4, 8, 16

Group1: 16 + 2 = 18
Group2: 4 + 8 = 12

Difference = 6
```

---

### Case 2: `n = 6`

```text id="p3v7kx"
Coins: 2,4,8,16,32,64

Group1: 64 + 2 + 4 = 70
Group2: 8 + 16 + 32 = 56

Difference = 14
```

---

### Case 3: `n = 8`

```text id="x8k2mz"
Group1: 256 + 2 + 4 + 8 = 270
Group2: 16 + 32 + 64 + 128 = 240

Difference = 30
```

---

## Complexity Analysis

### Time Complexity

O(n) per test case

* Loop through coins

---

### Space Complexity

O(1)

* Only variables used

---

## Solution Explanation

The solution strategically splits the coins:

* One group gets the largest coin and smallest ones
* Other group gets remaining medium-sized coins

This ensures maximum imbalance.

---

## Full Solution

### C++ Implementation

```cpp id="6n3k9z"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input n
        int n;
        cin >> n;

        // First group sum (largest + smallest coins)
        long long sum1 = 1LL << n;

        // Second group sum
        long long sum2 = 0;

        // Add smallest coins to sum1
        for(int i = 1; i < n/2; i++) {
            sum1 += (1LL << i);
        }

        // Add remaining coins to sum2
        for(int i = n/2; i < n; i++) {
            sum2 += (1LL << i);
        }

        // Output absolute difference
        cout << abs(sum1 - sum2) << "\n";
    }

    return 0;
}
```

---

## Test Cases Analysis

| n | Group1 (sum1) | Group2 (sum2) | Difference |
| - | ------------- | ------------- | ---------- |
| 2 | 4             | 2             | 2          |
| 4 | 18            | 12            | 6          |
| 6 | 70            | 56            | 14         |
| 8 | 270           | 240           | 30         |

---

## Edge Cases to Consider

* Smallest valid `n = 2`
* Large values (`n = 30`)
* Equal group sizes

---

## Common Test Cases

* `n = 2`
* `n = 4`
* `n = 8`

---

## Common Mistakes to Avoid

* Including wrong indices in groups
* Forgetting largest coin in group1
* Using incorrect power calculation

---

## Interview Relevance

* Greedy strategy
* Bit manipulation (`2^i`)
* Optimization thinking

---

## What This Problem Teaches

* Strategic partitioning
* Using powers efficiently
* Maximizing differences

---

## Key Takeaways

* Largest element dominates result
* Grouping strategy matters
* Bit operations simplify powers

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Greedy logic
* Mathematical reasoning
* Efficient computation