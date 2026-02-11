# 1371A_Magical_Sticks

## Platform

Codeforces

## Problem Link

[A. Magical Sticks](https://codeforces.com/problemset/problem/1371/A)

## Problem Statement

You are given an integer `n` representing the number of sticks.

You can perform the following operation any number of times:

* Take **two sticks** and combine them into **one stick**.

Your task is to determine the **minimum number of sticks remaining** after performing the operation optimally.

## Input Format

* The first line contains an integer `t`, the number of test cases
* For each test case:

  * A single integer `n`

## Output Format

* For each test case, print the minimum number of sticks remaining

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

* `n = 1` → No operation possible → Result = 1
* `n = 2` → Combine two sticks → 1 stick remains
* `n = 3` → Combine two sticks → 2 sticks remain

Output

```
1
1
2
```

---

### Example 2

Input

```
2
4
5
```

Explanation

* `n = 4` → Combine pairs → 2 sticks remain
* `n = 5` → Combine two pairs → 3 sticks remain

Output

```
2
3
```

## Approach

**Mathematical Observation (Ceiling Division)**

## Intuition

Each operation reduces the number of sticks by **1**, because:

* 2 sticks → 1 stick

This means:

* Every pair contributes to one resulting stick
* If `n` is even:

  * Result = `n / 2`
* If `n` is odd:

  * One stick remains unpaired
  * Result = `n / 2 + 1`

This is equivalent to:

```
ceil(n / 2)
```

Which can be computed as:

```
(n + 1) / 2
```

using integer arithmetic.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read `n`
  * Compute `(n + 1) / 2`
  * Print the result

## Visual Walkthrough

### Case 1: `n = 6`

```
Pairs: (2,2,2)
Result = 3
```

---

### Case 2: `n = 5`

```
Pairs: (2,2)
One leftover stick
Result = 3
```

---

### Case 3: `n = 1`

```
No pairing possible
Result = 1
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case

Only constant-time arithmetic is performed.

### Space Complexity

**O(1)**

No additional memory is used.

## Solution Explanation

The solution relies on a direct mathematical formula.

Instead of simulating operations, it calculates the result using ceiling division:

```
(n + 1) / 2
```

This guarantees the minimum number of sticks remaining after combining as many pairs as possible.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int n;
        cin >> n;

        // Minimum sticks remaining after optimal operations
        cout << (n + 1) / 2 << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n | Calculation | Output |
| - | ----------- | ------ |
| 1 | (1+1)/2 = 1 | 1      |
| 2 | (2+1)/2 = 1 | 1      |
| 3 | (3+1)/2 = 2 | 2      |
| 4 | (4+1)/2 = 2 | 2      |
| 5 | (5+1)/2 = 3 | 3      |

## Edge Cases to Consider

* `n = 1`
* Large value of `n` (`10^9`)
* Even vs odd values of `n`

## Common Test Cases

* Small values of `n`
* Large input sizes with multiple test cases
* Random even and odd values

## Common Mistakes to Avoid

* Using `n / 2` instead of ceiling division
* Overcomplicating with simulation
* Forgetting integer arithmetic behavior

## Interview Relevance

* Tests mathematical reasoning
* Evaluates understanding of integer division
* Common pattern for ceiling-based problems

## What This Problem Teaches

* Recognizing mathematical patterns
* Using ceiling division efficiently
* Avoiding unnecessary simulation

## Key Takeaways

* Many greedy operations reduce to simple formulas
* Ceiling division is a common competitive programming trick
* Always look for mathematical simplifications

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It requires basic arithmetic reasoning and careful observation, making it a standard beginner-level competitive programming task.