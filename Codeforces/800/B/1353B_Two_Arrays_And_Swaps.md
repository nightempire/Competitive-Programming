# B. Two Arrays And Swaps

## Platform

Codeforces

## Problem Link

[B. Two Arrays And Swaps](https://codeforces.com/problemset/problem/1353/B)

## Problem Statement

You are given multiple test cases.
For each test case, you are given:

* An integer `n`, the size of two arrays
* An integer `k`, the maximum number of swaps allowed
* Two integer arrays `a` and `b`, each of length `n`

You may perform **at most `k` swaps**, where each swap consists of choosing one element from array `a` and one element from array `b` and swapping them.

Your goal is to **maximize the sum of array `a`** after performing at most `k` swaps.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * Two integers `n` and `k`
  * A line with `n` integers representing array `a`
  * A line with `n` integers representing array `b`

## Output Format

For each test case, print a single integer — the **maximum possible sum of array `a`** after at most `k` swaps.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 30`
* `0 ≤ k ≤ n`
* `0 ≤ a[i], b[i] ≤ 100`

## Examples

### Example 1

Input

```
1
5 3
1 2 5 4 3
5 5 6 6 5
```

Explanation

After sorting:

```
a = [1, 2, 3, 4, 5]
b = [6, 6, 5, 5, 5]
```

Swaps:

```
1 ↔ 6
2 ↔ 6
3 ↔ 5
```

Final `a`:

```
[6, 6, 5, 4, 5]
```

Sum:

```
26
```

Output

```
26
```

### Example 2

Input

```
1
3 1
1 1 1
2 2 2
```

Explanation

One swap improves the smallest element of `a`.

Final `a`:

```
[2, 1, 1]
```

Sum:

```
4
```

Output

```
4
```

## Approach

Greedy strategy using sorting.

## Intuition

To maximize the sum of array `a`:

* Replace the **smallest elements in `a`** with the **largest elements in `b`**
* Perform this replacement only if it increases the value in `a`
* Limit the number of such improvements to at most `k`

Sorting both arrays enables direct, optimal comparisons.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read `n` and `k`
  * Read arrays `a` and `b`
  * Sort array `a` in ascending order
  * Sort array `b` in descending order
  * For the first `k` positions:

    * If `a[i] < b[i]`, replace `a[i]` with `b[i]`
  * Compute and print the sum of array `a`

## Visual Walkthrough

### Test Case 1

Input:

```
a = [1, 2, 5, 4, 3]
b = [5, 5, 6, 6, 5]
k = 3
```

Sorted:

```
a = [1, 2, 3, 4, 5]
b = [6, 6, 5, 5, 5]
```

Swap comparisons:

```
1 < 6 → replace
2 < 6 → replace
3 < 5 → replace
```

Final `a`:

```
[6, 6, 5, 4, 5]
```

---

### Test Case 2

Input:

```
a = [1, 1, 1]
b = [2, 2, 2]
k = 1
```

Swap:

```
1 < 2 → replace
```

Final `a`:

```
[2, 1, 1]
```

## Complexity Analysis

### Time Complexity

O(n log n) per test case

Sorting both arrays dominates the runtime.

### Space Complexity

O(1)

Sorting is done in-place, and only constant extra variables are used.

## Solution Explanation

The solution greedily improves the smallest elements of array `a` by swapping them with the largest available elements from array `b`.

By sorting both arrays appropriately, each potential swap is guaranteed to provide the maximum benefit, and unnecessary swaps are avoided.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while (t--) {

        // Size of arrays and maximum swaps
        int n, k;
        cin >> n >> k;

        // Arrays a and b
        int a[n], b[n];

        // Read array a
        for (int i = 0; i < n; i++)
            cin >> a[i];

        // Read array b
        for (int i = 0; i < n; i++)
            cin >> b[i];

        // Sort a in ascending order
        sort(a, a + n);

        // Sort b in descending order
        sort(b, b + n, greater<int>());

        // Perform at most k beneficial swaps
        for (int i = 0; i < k; i++) {
            if (a[i] < b[i]) {
                a[i] = b[i];
            }
        }

        // Calculate the sum of array a
        int sum = 0;
        for (int num : a)
            sum += num;

        // Output the result
        cout << sum << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n | k | a           | b           | Output |
| - | - | ----------- | ----------- | ------ |
| 5 | 3 | [1,2,3,4,5] | [6,6,5,5,5] | 26     |
| 3 | 1 | [1,1,1]     | [2,2,2]     | 4      |
| 4 | 0 | [1,2,3,4]   | [10,9,8,7]  | 10     |
| 2 | 2 | [1,2]       | [3,4]       | 7      |

## Edge Cases to Consider

* `k = 0` (no swaps allowed)
* Arrays already optimal
* All elements in `b` smaller than `a`

## Common Test Cases

* Small `n` with large values
* `k = n`
* Arrays with equal values

## Common Mistakes to Avoid

* Forgetting to sort arrays
* Swapping without checking benefit
* Exceeding `k` swaps

## Interview Relevance

* Demonstrates greedy optimization
* Tests sorting and comparison logic
* Common array-manipulation problem

## What This Problem Teaches

* Greedy decision-making
* Maximizing outcomes with limited operations
* Efficient use of sorting

## Key Takeaways

* Always swap only when beneficial
* Sorting simplifies optimal pairing
* Greedy strategies can yield optimal results

## Problem Difficulty Analysis

This is a **Medium-level (B)** problem.
It requires recognizing a greedy optimization strategy and implementing it efficiently.