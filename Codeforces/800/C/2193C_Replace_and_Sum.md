# C. Replace and Sum

## Platform

Codeforces

## Problem Link

[C. Replace and Sum](https://codeforces.com/problemset/problem/1931/C)

## Problem Statement

You are given two integer arrays of length `n` and a number of queries.

For each index `i`, you are allowed to **replace the element of the first array with the maximum of the two arrays at that index**.

After performing all replacements, you must process multiple range sum queries on the transformed array.

Each query asks for the **sum of elements in a given subarray**.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * A line containing two integers `n` and `q`.
  * A line containing `n` integers — the first array.
  * A line containing `n` integers — the second array.
  * `q` lines follow, each containing two integers `l` and `r`.

## Output Format

For each test case, output `q` integers — the answers to the range sum queries — separated by spaces.

Each test case output should appear on a new line.

## Constraints

* `1 ≤ t ≤ 10⁴`
* `1 ≤ n, q ≤ 2 × 10⁵`
* `0 ≤ ai, bi ≤ 10⁹`
* `1 ≤ l ≤ r ≤ n`
* The sum of `n` and `q` over all test cases does not exceed `2 × 10⁵`

## Examples

### Example 1

Input

```
1
5 3
1 2 3 4 5
5 4 3 2 1
1 3
2 5
1 5
```

Explanation

After replacement:

```
max(1,5) = 5
max(2,4) = 4
max(3,3) = 3
max(4,2) = 4
max(5,1) = 5
```

Array becomes:

```
5 4 3 4 5
```

After enforcing suffix maximum:

```
5 5 5 5 5
```

Prefix sum array:

```
5 10 15 20 25
```

Queries:

* `1 3` → `15`
* `2 5` → `20`
* `1 5` → `25`

Output

```
15 20 25
```

### Example 2

Input

```
1
3 1
2 2 2
1 1 1
1 3
```

Explanation

Replacement does not change the array.

Prefix sum:

```
2 4 6
```

Query result:

```
6
```

## Approach

**Greedy replacement + suffix maximum + prefix sum**

## Intuition

To maximize future range sums efficiently:

* Each element should be at least the maximum value seen to its right.
* This ensures that any subarray sum query reflects the optimal replacement strategy.

Once the array is transformed, prefix sums allow constant-time range sum queries.

## Algorithm Steps

* Read the number of test cases.
* For each test case:

  * Read `n` and `q`.
  * Read the first array.
  * Read the second array and replace each element with the maximum of the two.
  * Traverse from right to left to enforce the **suffix maximum property**.
  * Build a prefix sum array.
  * For each query:

    * Output the range sum using prefix sums.

## Visual Walkthrough

### Case 1

Initial arrays:

```
A: 1 2 3 4 5
B: 5 4 3 2 1
```

After replacement:

```
5 4 3 4 5
```

Suffix maximum enforced:

```
5 5 5 5 5
```

Prefix sum:

```
5 10 15 20 25
```

Query `(2,5)`:

```
25 − 5 = 20
```

---

### Case 2

Arrays:

```
A: 2 2 2
B: 1 1 1
```

After processing:

```
2 2 2
```

Prefix sum:

```
2 4 6
```

Query `(1,3)` → `6`

## Complexity Analysis

### Time Complexity

**O(n + q) per test case**

* Replacement: `O(n)`
* Suffix maximum pass: `O(n)`
* Prefix sum construction: `O(n)`
* Queries: `O(q)`

### Space Complexity

**O(1)** (excluding input array)

All transformations are done in-place.

## Solution Explanation

The solution ensures that each element reflects the maximum value it can contribute to future sums by propagating the largest values leftwards.
Prefix sums then enable efficient query processing without recomputation.

This approach is optimal given the constraints and avoids repeated summation.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Enable fast I/O
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    // Number of test cases
    int t;
    cin >> t;

    while (t--) {

        // n -> array size
        // q -> number of queries
        int n, q;
        cin >> n >> q;

        // Array with extra space for prefix sum convenience
        int nums[n + 1];

        // Sentinel value
        nums[n] = 0;

        // Read first array
        for (int i = 0; i < n; i++) {
            cin >> nums[i];
        }

        // Read second array and replace with max
        for (int i = 0; i < n; i++) {
            int num;
            cin >> num;

            // Replace with maximum value
            if (num > nums[i]) {
                nums[i] = num;
            }
        }

        // Enforce suffix maximum property
        for (int i = n - 2; i >= 0; i--) {
            if (nums[i] < nums[i + 1]) {
                nums[i] = nums[i + 1];
            }
        }

        // Build prefix sum array
        for (int i = 1; i <= n; i++) {
            nums[i] += nums[i - 1];
        }

        // Process range sum queries
        while (q--) {
            int l, r;
            cin >> l >> r;

            // Output sum from l to r
            cout << nums[r - 1] - (l - 2 < 0 ? 0 : nums[l - 2]) << " ";
        }

        cout << "\n";
    }

    return 0;
}
```

## Test Cases Analysis

| n | Queries | Final Array | Query | Output |
| - | ------- | ----------- | ----- | ------ |
| 5 | 3       | 5 5 5 5 5   | 1 3   | 15     |
| 5 | 3       | 5 5 5 5 5   | 2 5   | 20     |
| 3 | 1       | 2 2 2       | 1 3   | 6      |
| 1 | 1       | x           | 1 1   | x      |

## Edge Cases to Consider

* `n = 1`
* All elements already equal
* Second array strictly smaller
* Queries covering single elements

## Common Test Cases

* Full range queries
* Single index queries
* Mixed increasing and decreasing arrays

## Common Mistakes to Avoid

* Forgetting suffix maximum propagation
* Incorrect prefix sum indexing
* Off-by-one errors in range queries

## Interview Relevance

* Demonstrates prefix sum usage
* Tests greedy preprocessing
* Common pattern in range query problems

## What This Problem Teaches

* Combining greedy preprocessing with prefix sums
* Efficient query handling
* In-place array transformations

## Key Takeaways

* Preprocessing can drastically reduce query cost
* Suffix maximums ensure optimal value propagation
* Prefix sums are essential for fast range queries

## Problem Difficulty Analysis

This is a **Medium-level** problem.

It requires careful preprocessing logic and correct indexing, making it suitable for competitive programming and technical interviews.