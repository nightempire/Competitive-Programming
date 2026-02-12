# 1788A_One_and_Two

## Platform

Codeforces

## Problem Link

[A. One and Two](https://codeforces.com/problemset/problem/1788/A)

## Problem Statement

You are given an array consisting only of integers `1` and `2`.

Your task is to find an index `i` such that:

* The number of `2`s in the prefix `[0 … i]`
* Is equal to
* The number of `2`s in the suffix `[i+1 … n-1]`

If such an index exists, print `i + 1` (1-based index).
If no such index exists, print `-1`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * An integer `n`
  * An array of `n` integers, each either `1` or `2`

## Output Format

* For each test case, print:

  * The valid split position (1-based index), or
  * `-1` if no valid split exists

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 2 × 10^5`
* Each element is either `1` or `2`
* The sum of `n` across all test cases does not exceed `2 × 10^5`

## Examples

### Example 1

Input

```
1
4
1 2 1 2
```

Explanation

Total number of `2`s = 2

Half = 1

Prefix at index 1 (0-based):

```
[1, 2]
Number of 2s = 1
Suffix [1, 2]
Number of 2s = 1
```

Output

```
2
```

---

### Example 2

Input

```
1
3
2 2 2
```

Explanation

Total number of `2`s = 3 (odd)

Cannot split evenly.

Output

```
-1
```

---

### Example 3

Input

```
1
5
1 1 1 1 1
```

Explanation

Total number of `2`s = 0

Half = 0

Prefix at index 0 already satisfies condition.

Output

```
1
```

## Approach

**Counting and Prefix Traversal**

## Intuition

For the split to be valid:

* Total number of `2`s must be **even**
* Each side must contain exactly half of them

If the total count of `2`s is odd:

* It is impossible to divide equally → answer is `-1`

If even:

* Traverse the array
* Keep counting `2`s
* When prefix count equals half of total `2`s
* That position is the answer

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read `n`
  * Read array and count total number of `2`s
  * If total is odd:

    * Print `-1`
  * Else:

    * Traverse array again
    * Count prefix occurrences of `2`
    * When prefix count equals `total / 2`:

      * Print index + 1
      * Stop

## Visual Walkthrough

### Case 1: `1 2 1 2`

```
Total 2s = 2
Half = 1

Index 0 → 0 twos
Index 1 → 1 two → split here
```

Result = 2

---

### Case 2: `2 1 2 1 2 1`

```
Total 2s = 3 → odd
No valid split
```

Result = -1

---

### Case 3: `1 1 1`

```
Total 2s = 0
Half = 0

At index 0 → prefix 2s = 0 → valid
```

Result = 1

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Two linear passes:

* One for total count
* One for prefix search

### Space Complexity

**O(n)**

Array storage is required.

## Solution Explanation

The solution first determines feasibility by checking whether the total number of `2`s is even.

If feasible:

* It finds the earliest index where half of the `2`s are accumulated in the prefix.
* That ensures equal distribution between prefix and suffix.

This direct counting strategy ensures correctness and efficiency.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int n, two = 0;
        cin >> n;

        int nums[n];

        // Count total number of 2s
        for (int i = 0; i < n; i++) {
            cin >> nums[i];
            if (nums[i] == 2)
                two++;
        }

        // If total number of 2s is odd, split is impossible
        if (two & 1) {
            cout << -1 << '\n';
            continue;
        }

        int count = 0;

        // Find prefix where count of 2s equals half
        for (int i = 0; i < n; i++) {

            if (nums[i] == 2)
                ++count;

            if (count == two / 2) {
                cout << i + 1 << '\n';
                break;
            }
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Input Array | Total 2s | Output |
| ----------- | -------- | ------ |
| `1 2 1 2`   | 2        | 2      |
| `2 2 2`     | 3        | -1     |
| `1 1 1`     | 0        | 1      |
| `2 1 2 1`   | 2        | 1      |

## Edge Cases to Consider

* No `2`s in array
* Only one element
* All elements are `2`
* Large input sizes

## Common Test Cases

* Even number of `2`s
* Odd number of `2`s
* Mixed `1`s and `2`s

## Common Mistakes to Avoid

* Forgetting to check if total `2`s is odd
* Not using 1-based indexing in output
* Incorrect prefix count handling

## Interview Relevance

* Tests prefix sum logic
* Reinforces parity checks
* Evaluates careful condition handling

## What This Problem Teaches

* Splitting arrays based on frequency constraints
* Importance of feasibility checks
* Efficient linear traversal

## Key Takeaways

* Always verify possibility before searching for solution
* Prefix counting is a powerful technique
* Even simple problems require careful edge handling

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It relies on counting logic and basic array traversal, making it suitable for beginner-level competitive programming practice.