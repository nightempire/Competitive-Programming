# A_Make_it_Beautiful

## Platform

Codeforces

## Problem Link

[A. Make it Beautiful](https://codeforces.com/problemset/problem/1738/A)

## Problem Statement

You are given an array of `n` integers.

Your task is to determine whether it is possible to rearrange the array such that **no prefix of the array has the same sum as the remaining suffix**.

In other words, for every position `i` (`1 ≤ i < n`):

```
sum of first i elements ≠ sum of remaining elements
```

If such a rearrangement exists, print `"YES"` and output one possible rearranged array.
Otherwise, print `"NO"`.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * The first line contains an integer `n`.
  * The second line contains `n` integers representing the array.

## Output Format

For each test case:

* Print `"YES"` followed by a valid rearranged array if possible.
* Otherwise, print `"NO"`.

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n ≤ 100`
* `1 ≤ ai ≤ 10^9`

## Examples

### Example 1

Input

```
1
5
1 2 3 4 5
```

Explanation

Sorted array:

```
1 2 3 4 5
```

Rearranged:

```
1 5 2 4 3
```

Prefix sums:

| Prefix  | Sum |
| ------- | --- |
| 1       | 1   |
| 1 5     | 6   |
| 1 5 2   | 8   |
| 1 5 2 4 | 12  |

Remaining suffix sums are always different from these values.

Output

```
YES
1 5 2 4 3
```

---

### Example 2

Input

```
1
4
2 2 2 2
```

Explanation

All elements are equal.

Any rearrangement will produce identical prefix and suffix sums at some point.

Output

```
NO
```

---

### Example 3

Input

```
1
3
3 1 2
```

Explanation

Sorted:

```
1 2 3
```

Rearranged:

```
1 3 2
```

Prefix sums:

| Prefix | Sum |
| ------ | --- |
| 1      | 1   |
| 1 3    | 4   |

Remaining suffix sums:

```
3+2 = 5
2 = 2
```

No prefix sum equals suffix sum.

Output

```
YES
1 3 2
```

## Approach

Sorting with Two-Pointer Interleaving

## Intuition

If **all elements are equal**, then every permutation will have identical prefix/suffix structures, making it impossible to avoid equal sums.

However, if **at least two elements differ**, we can rearrange the array to prevent equal partitions.

A good strategy is:

* Sort the array.
* Alternate between the **smallest and largest elements**.

This spreads large values across the sequence, preventing prefix sums from matching suffix sums.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read `n`.
  * Read the array.
  * Sort the array.
  * If the smallest element equals the largest element:

    * Print `"NO"`.
  * Otherwise:

    * Print `"YES"`.
    * Use two pointers:

      * `left = 0`
      * `right = n - 1`
    * While `left < right`:

      * Print `nums[left]`
      * Print `nums[right]`
      * Move pointers inward.
    * If one element remains (`left == right`), print it.

## Visual Walkthrough

### Test Case 1

Input

```
1 2 3 4 5
```

Sorted

```
1 2 3 4 5
```

Rearranged

```
1 5 2 4 3
```

Construction

| Step | Left | Right | Output    |
| ---- | ---- | ----- | --------- |
| 1    | 1    | 5     | 1 5       |
| 2    | 2    | 4     | 1 5 2 4   |
| 3    | 3    | -     | 1 5 2 4 3 |

---

### Test Case 2

Input

```
2 2 2 2
```

Sorted

```
2 2 2 2
```

Smallest = Largest

```
Impossible
```

Output

```
NO
```

---

### Test Case 3

Input

```
3 1 2
```

Sorted

```
1 2 3
```

Rearranged

```
1 3 2
```

Construction

| Step | Output |
| ---- | ------ |
| 1    | 1 3    |
| 2    | 1 3 2  |

## Complexity Analysis

### Time Complexity

O(n log n)

Sorting dominates the runtime.

### Space Complexity

O(1)

The rearrangement is done directly using indices.

## Solution Explanation

The algorithm first sorts the array.

If all elements are identical, it immediately returns `"NO"` because no rearrangement can prevent equal prefix and suffix sums.

Otherwise, the array is rearranged using two pointers:

* smallest element
* largest element

This alternating pattern prevents balanced partitions and ensures that prefix sums grow unpredictably relative to suffix sums.

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

        // Size of array
        int n;
        cin >> n;

        // Array to store elements
        int nums[n];

        // Read array elements
        for (int i = 0; i < n; i++)
            cin >> nums[i];

        // Sort the array
        sort(nums, nums + n);

        // If all elements are equal
        if (nums[0] < nums[n - 1]) {

            cout << "YES\n";

            // Two-pointer approach
            int left = 0, right = n - 1;

            while (left < right) {

                // Print smallest and largest alternately
                cout << nums[left++] << " " << nums[right--] << " ";
            }

            // If one element remains
            if (left == right)
                cout << nums[left];

            cout << '\n';

        } else {

            // Impossible when all values are same
            cout << "NO\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Array     | Sorted    | Output Arrangement | Result |
| --------- | --------- | ------------------ | ------ |
| 1 2 3 4 5 | 1 2 3 4 5 | 1 5 2 4 3          | YES    |
| 2 2 2 2   | 2 2 2 2   | -                  | NO     |
| 3 1 2     | 1 2 3     | 1 3 2              | YES    |

## Edge Cases to Consider

* All numbers identical
* `n = 1`
* Two elements only
* Very large values

## Common Test Cases

* Increasing sequences
* All equal values
* Random arrays
* Small arrays (`n = 2` or `n = 3`)

## Common Mistakes to Avoid

* Forgetting to sort before rearranging
* Not checking the equal-elements case
* Incorrect pointer updates

## Interview Relevance

* Demonstrates array rearrangement techniques
* Introduces greedy construction strategies
* Tests understanding of prefix/suffix properties

## What This Problem Teaches

* Using sorting as preprocessing
* Two-pointer pattern for constructing permutations
* Avoiding undesired conditions through ordering

## Key Takeaways

* Rearrangement problems often rely on sorting
* Alternating extremes can prevent balanced partitions
* Always check trivial impossibility conditions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It primarily requires recognizing the impossibility case and constructing a valid permutation using a simple two-pointer technique after sorting.