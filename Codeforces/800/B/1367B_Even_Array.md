# B_Even_Array

## Platform

Codeforces

## Problem Link

[B. Even Array](https://codeforces.com/problemset/problem/1367/B)

## Problem Statement

You are given an array of integers.

An array is considered **even** if:

* Every element at an **even index** contains an **even number**
* Every element at an **odd index** contains an **odd number**

You are allowed to **swap any two elements** in the array.

Your task is to determine the **minimum number of swaps** required to make the array even.
If it is **impossible**, output `-1`.

Each test case is independent.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * An integer `n`, the size of the array.
  * `n` integers representing the array elements.

## Output Format

* For each test case:

  * Print the minimum number of swaps required to make the array even.
  * Print `-1` if it is not possible.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 40`
* `0 ≤ ai ≤ 1000`

## Examples

### Example 1

Input

```
1
4
3 2 7 6
```

Explanation

Indices and values:

```
Index:  0  1  2  3
Value:  3  2  7  6
```

Mismatches:

* Index 0 (even) → value 3 (odd)
* Index 1 (odd)  → value 2 (even)

Swapping these fixes both mismatches.

Output

```
1
```

---

### Example 2

Input

```
1
3
1 2 3
```

Explanation

* Mismatch count at even indices ≠ mismatch count at odd indices
* Cannot be balanced by swaps

Output

```
-1
```

## Approach

**Parity Mismatch Counting**

## Intuition

A valid array requires index parity to match value parity.

If an element is misplaced:

* An even index contains an odd number
* Or an odd index contains an even number

Each swap fixes **one even-index mismatch and one odd-index mismatch**.
Therefore:

* The number of mismatches at even indices must equal those at odd indices.
* Otherwise, it is impossible.

## Algorithm Steps

* Read number of test cases `t`.
* For each test case:

  * Read `n`.
  * Initialize counters:

    * `evenMismatch`
    * `oddMismatch`
  * For each index `i`:

    * Read the element `num`.
    * If index parity does not match value parity:

      * Increment corresponding mismatch counter.
  * If `evenMismatch != oddMismatch`, output `-1`.
  * Otherwise, output `oddMismatch` (minimum swaps).

## Visual Walkthrough

### Test Case: `3 2 7 6`

```
Index 0 (even) → 3 (odd)  → mismatch
Index 1 (odd)  → 2 (even) → mismatch
Index 2 (even) → 7 (odd)  → mismatch
Index 3 (odd)  → 6 (even) → mismatch
```

Counts:

```
evenMismatch = 2
oddMismatch  = 2
```

Each swap fixes one pair:

```
Minimum swaps = 2
```

---

### Test Case: `1 2 3`

```
Index 0 → 1 (odd)  → mismatch
Index 1 → 2 (even) → mismatch
Index 2 → 3 (odd)  → correct
```

Counts:

```
evenMismatch = 1
oddMismatch  = 1
```

Result:

```
1 swap required
```

## Complexity Analysis

### Time Complexity

**O(n) per test case**

* Each element is checked once.

### Space Complexity

**O(1)**

* Only integer counters are used.

## Solution Explanation

The solution identifies misplaced elements based on parity mismatch between indices and values.
Since each swap corrects exactly two mismatches (one even, one odd), feasibility depends on equal mismatch counts.

This logic ensures correctness and minimal operations.

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

        int oddMismatch = 0;
        int evenMismatch = 0;

        // Read array elements and count mismatches
        for (int i = 0; i < n; i++) {

            int num;
            cin >> num;

            // Check parity mismatch between index and value
            if ((i & 1) != (num & 1)) {

                // If index is odd
                if (i & 1)
                    oddMismatch++;
                else
                    evenMismatch++;
            }
        }

        // If mismatches cannot be paired, print -1
        if (oddMismatch != evenMismatch)
            cout << -1 << '\n';
        else
            cout << oddMismatch << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Array     | Even Mismatch | Odd Mismatch | Output |
| --------- | ------------- | ------------ | ------ |
| `3 2 7 6` | 2             | 2            | 2      |
| `1 2 3`   | 1             | 1            | 1      |
| `2 4 6`   | 0             | 0            | 0      |
| `1 3 5`   | 2             | 0            | -1     |

## Edge Cases to Consider

* Array already valid
* All elements mismatched
* Odd-length arrays

## Common Test Cases

* Alternating parity arrays
* Fully incorrect arrays
* Single-element arrays

## Common Mistakes to Avoid

* Counting only total mismatches
* Ignoring index parity
* Assuming swaps can fix unequal mismatches

## Interview Relevance

* Tests parity logic
* Demonstrates greedy reasoning
* Reinforces feasibility checks

## What This Problem Teaches

* Understanding swap constraints
* Matching problems via parity
* Efficient mismatch tracking

## Key Takeaways

* Swaps correct mismatches in pairs
* Feasibility checks are crucial
* Simple logic can avoid unnecessary operations

## Problem Difficulty Analysis

This is an **Easy-to-Medium** level problem.
It focuses on logical reasoning and parity analysis rather than complex algorithms.