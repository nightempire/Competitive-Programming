# A. Remove Smallest

## Platform

Codeforces

## Problem Link

[A. Remove Smallest](https://codeforces.com/problemset/problem/1399/A)

## Problem Statement

You are given an array of integers.

You can repeatedly remove the **smallest element** from the array.
After removing an element, the remaining elements shift accordingly.

The task is to determine whether it is possible to remove elements **one by one** such that at every step, the **difference between the smallest remaining elements is at most 1**.

If it is possible, print `"YES"`, otherwise print `"NO"`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case consists of:

  * An integer `n`, the size of the array
  * A line containing `n` integers

```
n
a1 a2 a3 ... an
```

## Output Format

For each test case, print `"YES"` or `"NO"`.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 100`
* `1 ≤ ai ≤ 100`

## Examples

### Example 1

Input

```
3
3
1 2 3
3
1 3 4
5
2 2 2 3 3
```

Explanation

* Test case 1: Differences are at most 1 → `YES`
* Test case 2: Difference between `1` and `3` is greater than 1 → `NO`
* Test case 3: All adjacent differences are ≤ 1 → `YES`

Output

```
YES
NO
YES
```

## Approach

**Sorting + Adjacent Difference Check**

## Intuition

If it is possible to remove elements one by one without violating the condition, then after sorting:

* Every **adjacent pair** must differ by **at most 1**

Why sorting works:

* Removing the smallest element repeatedly is equivalent to checking whether the numbers can be ordered so that no large gaps exist.
* A gap larger than `1` makes it impossible to maintain the required condition.

## Algorithm Steps

* Read the number of test cases
* For each test case:

  * Read `n` and the array
  * Sort the array
  * Traverse the array from index `1` to `n-1`
  * If any `nums[i] - nums[i-1] > 1`, mark as invalid
  * Print `"NO"` if invalid, otherwise `"YES"`

## Visual Walkthrough

Test case:

```
nums = [1, 3, 4]
```

After sorting:

```
[1, 3, 4]
```

Differences:

```
3 - 1 = 2  → invalid
```

Output:

```
NO
```

Another case:

```
nums = [2, 2, 3, 3]
```

Differences:

```
2-2 = 0
3-2 = 1
3-3 = 0
```

All valid → `YES`

## Complexity Analysis

### Time Complexity

O(n log n)

Sorting dominates the runtime.

### Space Complexity

O(1)

Only a fixed-size array and variables are used.

## Solution Explanation

The solution sorts the array so that comparisons become straightforward.
It then checks whether any adjacent elements differ by more than `1`.

If such a gap exists, it is impossible to remove elements while maintaining the constraint, so the answer is `"NO"`.
Otherwise, the answer is `"YES"`.

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

        // Size of the array
        int n;
        cin >> n;

        // Read the array elements
        int nums[n];
        for (int i = 0; i < n; i++) {
            cin >> nums[i];
        }

        // Sort the array to compare adjacent elements
        sort(nums, nums + n);

        // Flag to check validity
        bool flag = false;

        // Check differences between adjacent elements
        for (int i = 1; i < n; i++) {
            if (nums[i] - nums[i - 1] > 1) {
                flag = true;
                break;
            }
        }

        // Output result
        cout << (flag ? "NO\n" : "YES\n");
    }

    return 0;
}
```

## Test Cases Analysis

| Array        | Sorted       | Result |
| ------------ | ------------ | ------ |
| [1, 2, 3]    | [1, 2, 3]    | YES    |
| [1, 3, 4]    | [1, 3, 4]    | NO     |
| [2, 2, 3, 3] | [2, 2, 3, 3] | YES    |
| [1, 1, 1]    | [1, 1, 1]    | YES    |

## Edge Cases to Consider

* All elements are equal
* `n = 1`
* Large gaps between numbers

## Common Test Cases

* Consecutive integers
* Repeated values
* Arrays with one large gap

## Common Mistakes to Avoid

* Forgetting to sort the array
* Checking absolute differences unnecessarily
* Misinterpreting the removal condition

## Interview Relevance

* Tests sorting fundamentals
* Encourages reasoning instead of simulation
* Common greedy-style validation problem

## What This Problem Teaches

* Sorting simplifies many constraint checks
* Adjacent comparisons can validate global conditions
* Removing simulation often improves clarity and performance

## Key Takeaways

* Always check if sorting can simplify a problem
* Gaps in sorted data often indicate impossibility
* Clean logic is preferable to step-by-step simulation

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on array manipulation and logical validation, making it suitable for beginners and competitive programming practice.