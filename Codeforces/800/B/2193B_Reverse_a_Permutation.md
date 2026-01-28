# B. Reverse a Permutation

## Platform

Codeforces

## Problem Link

[B. Reverse a Permutation](https://codeforces.com/problemset/problem/1931/B)

## Problem Statement

You are given a **permutation of size `n`**.

The goal is to transform the permutation into a **descending permutation**:

```
n, n−1, n−2, … , 1
```

You are allowed to perform **at most one reverse operation** on a **contiguous subarray** of the permutation.

For each test case, output the resulting permutation after applying the required operation.

If the permutation already satisfies the required condition, output it as is.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * A single integer `n`, the size of the permutation.
  * A line containing `n` integers representing the permutation.

## Output Format

For each test case, print the resulting permutation after performing **at most one reverse operation**.

## Constraints

* `1 ≤ t ≤ 10⁴`
* `1 ≤ n ≤ 2 × 10⁵`
* The sum of `n` over all test cases does not exceed `2 × 10⁵`
* The array is a valid permutation of numbers from `1` to `n`

## Examples

### Example 1

Input

```
1
5
5 4 3 2 1
```

Explanation

The permutation is already in descending order.
No operation is required.

Output

```
5 4 3 2 1
```

### Example 2

Input

```
1
5
5 3 4 2 1
```

Explanation

Expected descending permutation:

```
5 4 3 2 1
```

The subarray `[3, 4]` is reversed to fix the order.

Output

```
5 4 3 2 1
```

### Example 3

Input

```
1
4
4 2 3 1
```

Explanation

Mismatch starts at index `1`.

Reversing the subarray `[2, 3]` restores the descending order.

Output

```
4 3 2 1
```

## Approach

**Greedy identification + single subarray reversal**

## Intuition

A correct descending permutation satisfies:

```
nums[i] = n − i
```

The first position where this condition fails marks the **start of the incorrect segment**.
The segment ends where the expected value for that start position appears.

Reversing exactly this segment fixes the permutation using **one operation**, which is optimal.

## Algorithm Steps

* Read the number of test cases.
* For each test case:

  * Read `n` and the permutation array.
  * Traverse the array to find the **first index** where `nums[i] ≠ n − i`.
  * Mark this index as `start`.
  * Continue scanning to find the index where the correct value for `start` appears.
  * Mark that index as `end`.
  * Reverse the subarray from `start` to `end`.
* Print the resulting permutation.

## Visual Walkthrough

### Case 1

```
n = 5
Permutation: 5 3 4 2 1
Expected:    5 4 3 2 1
```

Mismatch at index `1`.

Reverse subarray:

```
[3 4] → [4 3]
```

Result:

```
5 4 3 2 1
```

---

### Case 2

```
n = 4
Permutation: 4 2 3 1
Expected:    4 3 2 1
```

Reverse:

```
[2 3] → [3 2]
```

Result:

```
4 3 2 1
```

---

### Case 3

```
n = 3
Permutation: 3 2 1
```

Already valid → no operation.

## Complexity Analysis

### Time Complexity

**O(n) per test case**

Each element is scanned at most once, and at most one reverse operation is performed.

### Space Complexity

**O(1)**

The reversal is done in-place using constant extra space.

## Solution Explanation

The solution identifies the smallest contiguous segment that breaks the descending order condition.
Reversing only this segment restores the required permutation efficiently.

This greedy strategy works because a permutation can be fixed using **at most one reversal**.

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

        // Size of the permutation
        int n;
        cin >> n;

        // Array to store permutation
        int nums[n];

        // start and end indices of the segment to reverse
        int start = -1, end = -1;

        // Flag to mark when mismatch is found
        bool flag = false;

        // Read permutation and detect mismatch segment
        for (int i = 0; i < n; i++) {
            cin >> nums[i];

            // Identify first index where descending order breaks
            if (!flag && nums[i] != n - i) {
                flag = true;
                start = i;
            }

            // Find the position where correct value appears
            if (flag && nums[i] == n - start) {
                end = i;
            }
        }

        // Reverse the identified segment if needed
        if (flag) {
            while (start < end) {
                int temp = nums[start];
                nums[start] = nums[end];
                nums[end] = temp;
                start++;
                end--;
            }
        }

        // Output the resulting permutation
        for (int i = 0; i < n; i++) {
            cout << nums[i] << " ";
        }
        cout << "\n";
    }

    return 0;
}
```

## Test Cases Analysis

| Input Permutation | n | Reverse Segment | Output    |
| ----------------- | - | --------------- | --------- |
| 5 4 3 2 1         | 5 | None            | 5 4 3 2 1 |
| 5 3 4 2 1         | 5 | [3,4]           | 5 4 3 2 1 |
| 4 2 3 1           | 4 | [2,3]           | 4 3 2 1   |
| 1                 | 1 | None            | 1         |

## Edge Cases to Consider

* `n = 1`
* Already descending permutation
* Reversal segment of length 2
* Reversal segment spans the entire array

## Common Test Cases

* Single mismatch segment
* No mismatch at all
* Entire permutation reversed

## Common Mistakes to Avoid

* Reversing multiple segments
* Incorrect expected value calculation (`n - i`)
* Forgetting that indices are zero-based

## Interview Relevance

* Tests greedy reasoning
* Evaluates array manipulation skills
* Common permutation-handling pattern

## What This Problem Teaches

* Identifying minimal correction segments
* Efficient in-place reversal
* Using problem constraints to simplify logic

## Key Takeaways

* A single reverse can fix structured permutations
* Greedy boundary detection is powerful
* Always compare against expected positions

## Problem Difficulty Analysis

This is an **Easy-to-Medium level** problem.

It requires careful observation of permutation properties and precise implementation, making it suitable for contest beginners progressing to intermediate problems.