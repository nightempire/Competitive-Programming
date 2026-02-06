# A_Jagged_Swaps

## Platform

Codeforces

## Problem Link

[A. Jagged Swaps](https://codeforces.com/problemset/problem/1896/A)

## Problem Statement

You are given multiple test cases.
In each test case:

* An integer `n`, the size of an array
* An array of `n` integers

You are allowed to perform a specific type of swap operation (as defined in the problem) any number of times.

Your task is to determine whether it is **possible to make the array sorted in non-decreasing order** using the allowed operations.

For each test case, print `"YES"` if it is possible, otherwise print `"NO"`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`
  * The second line contains `n` integers

## Output Format

For each test case, print:

* `"YES"` if the array can be sorted
* `"NO"` otherwise

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 10^5`
* `1 ≤ nums[i] ≤ 10^9`
* Sum of `n` over all test cases does not exceed limits

## Examples

### Example 1

Input

```
3
3
1 3 2
4
2 1 3 4
5
1 2 3 4 5
```

Explanation

* Test case 1:

  * First element is `1`
  * Valid → `YES`
* Test case 2:

  * First element is not `1`
  * Invalid → `NO`
* Test case 3:

  * First element is `1`
  * Valid → `YES`

Output

```
YES
NO
YES
```

### Example 2

Input

```
2
1
1
2
5 4
```

Explanation

* Test case 1:

  * Single element `1` → already sorted
* Test case 2:

  * First element is `5` ≠ `1` → cannot be sorted

Output

```
YES
NO
```

## Approach

**Direct validation using the first element**

## Intuition

From the properties of the allowed swap operations:

* The element `1` cannot be moved to the front unless it is **already at index 0**
* If the first element is not `1`, then `1` will always remain somewhere to the right
* Hence, the array can never become fully sorted

Therefore:

* If `nums[0] == 1` → sorting is possible
* Otherwise → sorting is impossible

## Algorithm Steps

* Read integer `t`
* For each test case:

  * Read integer `n`
  * Read the array `nums`
  * If `nums[0] == 1`, print `"YES"`
  * Otherwise, print `"NO"`

## Visual Walkthrough

### Test Case 1

Input:

```
[1, 4, 3, 2]
```

Observation:

```
First element = 1
```

Result:

```
YES
```

---

### Test Case 2

Input:

```
[3, 1, 2]
```

Observation:

```
First element ≠ 1
1 cannot move to front
```

Result:

```
NO
```

---

### Test Case 3

Input:

```
[1]
```

Observation:

```
Already sorted
```

Result:

```
YES
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case

Only the first element is checked.

### Space Complexity

**O(1)**

No extra memory is used.

## Solution Explanation

The solution relies on a crucial invariant of the allowed swap operations:
the smallest element (`1`) must already be at the first position for the array to be sortable.

By checking this single condition, the problem is solved efficiently without any unnecessary processing.

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
        for (int i = 0; i < n; i++) {
            cin >> nums[i];
        }

        // Check if the first element is 1
        if (nums[0] == 1) {
            cout << "YES\n";
        } else {
            cout << "NO\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Input Array | nums[0] | Output |
| --------- | ----------- | ------- | ------ |
| 1         | [1,3,2]     | 1       | YES    |
| 2         | [2,1,3,4]   | 2       | NO     |
| 3         | [1,2,3,4,5] | 1       | YES    |
| 4         | [5,4]       | 5       | NO     |

## Edge Cases to Consider

* Single-element arrays
* Already sorted arrays
* Arrays where `1` appears but not at index `0`

## Common Test Cases

* `1` at the front
* `1` not at the front
* Large arrays with random values

## Common Mistakes to Avoid

* Trying to simulate swaps unnecessarily
* Sorting the array explicitly
* Ignoring the position of the smallest element

## Interview Relevance

* Tests understanding of invariants
* Evaluates ability to reduce a problem to a simple condition
* Good example of observation-based optimization

## What This Problem Teaches

* Identifying immovable constraints
* Simplifying problems using key observations
* Avoiding brute-force simulations

## Key Takeaways

* Sometimes a single condition determines feasibility
* Understanding problem constraints is critical
* Efficient solutions often come from strong observations

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on logical insight rather than implementation complexity.