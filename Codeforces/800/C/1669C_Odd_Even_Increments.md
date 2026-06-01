## 1669C. Odd/Even Increments

## Platform

Codeforces

## Problem Link

[A. Odd/Even Increments](https://codeforces.com/problemset/problem/1669/C)

## Problem Statement

You are given an array `a` of length `n`.

You may perform the following operation any number of times:

* Choose all elements at **odd indices** and increase them by `1`, or
* Choose all elements at **even indices** and increase them by `1`.

Determine whether it is possible to make **all elements of the array have the same parity** (all odd or all even) after performing any number of operations.

> Note: The problem uses **1-based indexing**.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`.
  * The second line contains `n` integers `a₁, a₂, ..., aₙ`.

## Output Format

* Print `"YES"` if it is possible to make all elements have the same parity.
* Otherwise, print `"NO"`.

## Constraints

* `1 ≤ t ≤ 10^4`
* `2 ≤ n ≤ 50`
* `1 ≤ a[i] ≤ 10^3`

## Examples

### Example 1

Input

```text
3
4
1 2 1 2
4
2 4 6 8
3
1 2 3
```

Explanation

For the first array:

```text
Odd positions  : 1, 1
Even positions : 2, 2
```

Parity within each position group is consistent.

Output

```text
YES
YES
YES
```

---

### Example 2

Input

```text
2
4
1 2 2 4
5
1 3 5 7 2
```

Explanation

First array:

```text
Odd positions:
1, 2
```

Parities differ.

Output

```text
NO
NO
```

---

### Example 3

Input

```text
1
6
5 8 7 10 9 12
```

Explanation

```text
Odd positions  : 5, 7, 9   → all odd
Even positions : 8,10,12   → all even
```

Condition satisfied.

Output

```text
YES
```

## Approach

Parity Observation

## Intuition

When we increment all elements at odd positions by `1`, their parity flips together.

Similarly, incrementing all elements at even positions flips the parity of all even-positioned elements together.

Therefore:

* All elements at odd indices must initially have the same parity.
* All elements at even indices must initially have the same parity.

If this condition holds, we can make the entire array have uniform parity through allowed operations.

The provided solution checks this by verifying:

```text
a[i] and a[i-2]
```

have the same parity for every valid `i`.

## Algorithm Steps

* Read `t`.
* For each test case:

  * Read `n`.
  * Read the array.
  * Compare parity of every element with the element two positions before it.
  * If any parity mismatch occurs:

    * Mark answer as `"NO"`.
  * Otherwise:

    * Answer is `"YES"`.

## Visual Walkthrough

### Case 1

```text
Array = [1, 2, 1, 2]
```

Compare:

```text
a[0] vs a[2]
1 vs 1 → same parity

a[1] vs a[3]
2 vs 2 → same parity
```

Result:

```text
YES
```

---

### Case 2

```text
Array = [1, 2, 2, 4]
```

Compare:

```text
a[0] vs a[2]
1 vs 2
odd vs even → mismatch
```

Result:

```text
NO
```

---

### Case 3

```text
Array = [5, 8, 7, 10, 9, 12]
```

Compare:

```text
5 vs 7 → same parity
7 vs 9 → same parity

8 vs 10 → same parity
10 vs 12 → same parity
```

Result:

```text
YES
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each element is checked once after reading.

### Space Complexity

**O(n)**

The solution stores the array before performing parity checks.

## Solution Explanation

The operation affects all odd-indexed or all even-indexed elements simultaneously.

Because of this, elements belonging to the same index parity group must already share the same parity. Otherwise, they can never be made equal in parity through the allowed operations.

The solution verifies this by comparing each element with the one located two positions before it. If every such comparison has matching parity, the answer is `"YES"`.

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

        // Size of array
        int n;
        cin >> n;

        // Store array elements
        int nums[n];

        // Read first two elements
        cin >> nums[0] >> nums[1];

        // Assume answer is YES initially
        bool flag = true;

        // Read remaining elements
        for(int i = 2; i < n; i++) {

            cin >> nums[i];

            // Elements at positions differing by 2
            // belong to the same parity index group
            if((nums[i - 2] & 1) != (nums[i] & 1)) {
                flag = false;
            }
        }

        // Print result
        cout << (flag ? "YES\n" : "NO\n");
    }

    return 0;
}
```

## Test Cases Analysis

| Array           | Odd Position Parity Consistent | Even Position Parity Consistent | Output |
| --------------- | ------------------------------ | ------------------------------- | ------ |
| [1,2,1,2]       | Yes                            | Yes                             | YES    |
| [2,4,6,8]       | Yes                            | Yes                             | YES    |
| [1,2,2,4]       | No                             | Yes                             | NO     |
| [5,8,7,10,9,12] | Yes                            | Yes                             | YES    |
| [1,3,5,7,2]     | Yes                            | No                              | NO     |

## Edge Cases to Consider

* Minimum array size (`n = 2`)
* All elements odd
* All elements even
* Only odd-position group invalid
* Only even-position group invalid

## Common Test Cases

* Alternating odd/even values
* Uniform parity arrays
* Mixed parity groups
* Large valid arrays

## Common Mistakes to Avoid

* Comparing adjacent elements instead of elements two positions apart.
* Forgetting that the problem uses 1-based indexing conceptually.
* Assuming all array elements must initially have the same parity.

## Interview Relevance

* Tests parity reasoning.
* Demonstrates invariant-based thinking.
* Shows how operations affect groups rather than individual elements.

## What This Problem Teaches

* Using parity as an invariant.
* Understanding effects of bulk update operations.
* Simplifying problems through observations.

## Key Takeaways

* Odd-indexed elements form one parity group.
* Even-indexed elements form another parity group.
* Checking parity consistency within each group is sufficient.

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The implementation is simple once the parity observation is identified. The main challenge is recognizing that operations preserve the relative parity relationships within the odd-indexed and even-indexed groups.