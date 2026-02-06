# A_Desorting

## Platform

Codeforces

## Problem Link

[A. Desorting](https://codeforces.com/problemset/problem/1853/A)

## Problem Statement

You are given multiple test cases.
In each test case:

* An integer `n`, the length of an array.
* A sequence of `n` integers.

Your task is to determine the **minimum number of moves** required to make the array *not sorted in non-decreasing order*.

A move consists of selecting an element and **increasing its value by any positive integer**.

If the array is already **not strictly non-decreasing**, the answer is `0`.

Otherwise, compute the minimum number of moves needed so that the array becomes not sorted (i.e., has at least one position where a value becomes less than its previous value).

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`
  * The second line contains `n` integers

## Output Format

For each test case, print a single integer — the minimum number of moves required.

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 10^4`
* `2 ≤ n ≤ 50`
* `1 ≤ nums[i] ≤ 10^9`

## Examples

### Example 1

Input

```
3
3
1 2 3
3
3 2 1
4
5 5 5 5
```

Explanation

* Test case 1:

  * Array is already sorted non-decreasing
  * Differences → 1,1 → minimum difference is 1
  * Moves needed = (1/2 + 1) = `1`
* Test case 2:

  * Not sorted → `0` moves required
* Test case 3:

  * All elements equal → differences are 0, minimum positive difference is 0
  * Moves needed = (0/2 + 1) = `1`

Output

```
1
0
1
```

### Example 2

Input

```
2
5
1 2 4 7 8
4
1 10 20 30
```

Output

```
2
6
```

## Approach

**Check sortedness and compute minimal increment requirement**

## Intuition

If the array is **already not non-decreasing**, no moves are needed — answer is `0`.

Otherwise:

* Compute the **minimum positive adjacent difference** between consecutive elements.
* Increasing a value by a number greater than half of this minimum difference will force a violation in the sorted property by making that element greater than the next in sequence.

Hence, the minimum number of moves required is:

```
floor(min_diff / 2) + 1
```

This guarantees you create a decrease at some position.

## Algorithm Steps

* Read integer `t`
* For each test case:

  * Read `n` and the array `nums`
  * Check whether there exists any index `i` such that `nums[i] > nums[i + 1]`

    * If yes → output `0`
  * Otherwise:

    * Track the minimum positive difference among `nums[i + 1] − nums[i]`
    * Compute result as `min_diff / 2 + 1`
    * Output the result

## Visual Walkthrough

### Test Case 1

Input:

```
[1, 2, 3]
```

Differences:

```
1, 1
```

Minimum difference:

```
1
```

Compute:

```
1/2 + 1 = 0 + 1 = 1
```

Output:

```
1
```

---

### Test Case 2

Input:

```
[3, 2, 1]
```

Check:

```
3 > 2 → not sorted
```

Output:

```
0
```

---

### Test Case 3

Input:

```
[5,5,5,5]
```

Differences:

```
0,0,0
```

Minimum positive difference is effectively 0

Compute:

```
0/2 + 1 = 1
```

Output:

```
1
```

---

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Linear scan through the array to check ordering and compute adjacent differences.

### Space Complexity

**O(1)**

Only a few local variables are used.

## Solution Explanation

The array is desorted by introducing a violation in the non-decreasing order.
If the array already has such a violation, no moves are required.

Otherwise, to guarantee violation, choose the smallest positive gap between adjacent elements and increase an element by enough to cross that gap, which always ensures a decrease at some adjacent pair.

Using adjacent differences avoids scanning all pairs unnecessarily.

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
        int nums[n];

        // Read the array
        for (int i = 0; i < n; i++) {
            cin >> nums[i];
        }

        bool flag = false;
        int mn = INT_MAX;

        // Check sortedness and compute adjacent differences
        for (int i = 1; i < n; i++) {

            // If any adjacent pair is decreasing,
            // the array is already not non-decreasing
            if (nums[i - 1] > nums[i]) {
                flag = true;
                break;
            } else {
                // Track minimum difference
                mn = min(mn, nums[i] - nums[i - 1]);
            }
        }

        // If array already desorted
        if (flag) {
            cout << "0\n";
        } else {
            // Compute minimum moves
            cout << mn / 2 + 1 << '\n';
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Input Array  | Sorted? | min_diff | Output |
| --------- | ------------ | ------- | -------- | ------ |
| 1         | [1,2,3]      | Yes     | 1        | 1      |
| 2         | [3,2,1]      | No      | —        | 0      |
| 3         | [5,5,5,5]    | Yes     | 0        | 1      |
| 4         | [1,2,4,7,8]  | Yes     | 1        | 1      |
| 5         | [1,10,20,30] | Yes     | 9,10,10  | 6      |

## Edge Cases to Consider

* Already desorted array
* All elements identical
* Large minimum differences

## Common Test Cases

* Small `n`
* Sorted arrays with increasing gaps
* Arrays with immediate desort conditions

## Common Mistakes to Avoid

* Using `<=` instead of `<` when checking sortedness
* Miscomputing minimum difference
* Assuming positive differences only

## Interview Relevance

* Tests array scanning and condition checking
* Requires careful boundary handling
* Involves simple math to compute required adjustments

## What This Problem Teaches

* How to detect sorted order
* How to induce specific order violations
* Using adjacent differences for problem solving

## Key Takeaways

* Simple checks can avoid heavy computation
* Edge case of equal elements requires care
* Desorting can be achieved with minimal moves

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes clean logic and correct branch handling rather than complex algorithms.