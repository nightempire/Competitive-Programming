## Platform

Codeforces

## Problem Link

[A. Unit Array](https://codeforces.com/problemset/problem/1834/A)

---

## Problem Statement

You are given an array `a` of size `n` consisting only of values `1` and `-1`.

You can perform the following operation any number of times:

* Choose any index `i` and **multiply `a[i]` by -1** (i.e., flip its sign).

Your goal is to make the array satisfy both conditions:

* The **sum of the array is non-negative**
* The **product of all elements is equal to 1**

Find the **minimum number of operations** required.

---

## Input Format

* The first line contains an integer `t` — number of test cases.
* For each test case:

  * The first line contains integer `n`
  * The second line contains `n` integers (`1` or `-1`)

---

## Output Format

For each test case, print a single integer — the minimum number of operations.

---

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 100`
* Each element is either `1` or `-1`

---

## Examples

### Example 1

Input

```
3
4
1 1 -1 -1
3
-1 -1 -1
2
1 -1
```

Explanation

* Case 1:

  * Negatives = 2, Positives = 2
  * Sum = 0 (valid), product = 1 → already valid

* Case 2:

  * Negatives = 3, Positives = 0
  * Convert one `-1 → 1`
  * New negatives = 2 → product = 1, sum ≥ 0

* Case 3:

  * Negatives = 1 → product = -1
  * Flip one → valid

Output

```
0
1
1
```

---

### Example 2

Input

```
2
5
-1 -1 -1 -1 -1
4
1 1 1 1
```

Explanation

* First case:

  * Negatives = 5
  * Convert until negatives ≤ positives → operations needed

* Second case:

  * Already valid

Output

```
3
0
```

---

## Approach

Greedy balancing with parity correction

---

## Intuition

Two conditions must be satisfied:

**Sum ≥ 0**

* Number of `1`s ≥ number of `-1`s
* i.e., `neg ≤ pos`

**Product = 1**

* Number of `-1`s must be **even**

---

So we proceed in two phases:

First, ensure **sum condition**:

* If `neg > pos`, convert some `-1 → 1`

Then, ensure **product condition**:

* If `neg` is odd → perform one extra flip

---

## Algorithm Steps

* Read `t`

* For each test case:

  * Read `n`
  * Count number of negative elements `neg`
  * Initialize operations `ops = 0`

* Step 1: Fix sum condition

  * While `neg > n - neg`:

    * Convert one `-1 → 1`
    * Decrease `neg`
    * Increment `ops`

* Step 2: Fix product condition

  * If `neg` is odd:

    * Increment `ops`

* Print `ops`

---

## Visual Walkthrough

### Case 1: `[-1, -1, -1]`

```
neg = 3, pos = 0

Step 1:
neg > pos → convert one
neg = 2, ops = 1

Step 2:
neg is even → OK

Result → 1 operation
```

---

### Case 2: `[1, -1]`

```
neg = 1, pos = 1

Step 1:
neg ≤ pos → OK

Step 2:
neg is odd → +1 operation

Result → 1 operation
```

---

### Case 3: `[-1, -1, 1, 1]`

```
neg = 2, pos = 2

Step 1:
Already balanced

Step 2:
neg even → OK

Result → 0 operations
```

---

## Complexity Analysis

### Time Complexity

O(n) per test case

* We only count negatives in one pass.

---

### Space Complexity

O(1)

* Only counters are used.

---

## Solution Explanation

The solution is based on maintaining two invariants:

* Balance between positive and negative values to ensure non-negative sum
* Even count of negative values to ensure product equals 1

The algorithm greedily reduces excess negatives and then adjusts parity if required. This guarantees minimal operations.

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

    // Process each test case
    while(t--) {

        // Size of array and count of negative numbers
        int n, neg = 0;
        cin >> n;

        // Read array elements and count negatives
        for(int i = 0; i < n; i++) {
            int num;
            cin >> num;

            // Count number of -1 values
            if(num < 0) {
                neg++;
            }
        }

        // Variable to store number of operations
        int ops = 0;

        // Step 1: Ensure sum is non-negative
        // Condition: negatives should not exceed positives
        while(neg > n - neg) {

            // Convert one -1 to 1
            neg--;

            // Increase operation count
            ops++;
        }

        // Step 2: Ensure product is 1
        // Condition: number of negatives must be even
        if(neg & 1) {

            // One extra operation needed to fix parity
            ops++;
        }

        // Output result
        cout << ops << '\n';
    }
}
```

---

## Test Cases Analysis

| n | Array          | Negatives | Operations | Reason                   |
| - | -------------- | --------- | ---------- | ------------------------ |
| 3 | -1 -1 -1       | 3         | 1          | Balance + parity         |
| 4 | 1 1 -1 -1      | 2         | 0          | Already valid            |
| 2 | 1 -1           | 1         | 1          | Fix parity               |
| 5 | -1 -1 -1 -1 -1 | 5         | 3          | Multiple balancing steps |

---

## Edge Cases to Consider

* All elements are `-1`
* All elements are `1`
* Single element array
* Odd number of negatives after balancing

---

## Common Test Cases

* `[-1]` → 1
* `[1]` → 0
* `[-1, -1]` → 0
* `[-1, 1, -1, 1]` → 0

---

## Common Mistakes to Avoid

* Forgetting to fix parity after balancing
* Miscalculating positives (`n - neg`)
* Using incorrect loop condition

---

## Interview Relevance

* Greedy decision making
* Handling multiple constraints simultaneously
* Understanding parity and invariants

---

## What This Problem Teaches

* How to convert constraints into conditions
* Balancing techniques in arrays
* Importance of parity in product problems

---

## Key Takeaways

* Two independent constraints must both be satisfied
* Greedy adjustment minimizes operations
* Always check parity after balancing

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on:

* Counting
* Greedy adjustments
* Logical reasoning

Well-suited for beginners and quick contest problems.