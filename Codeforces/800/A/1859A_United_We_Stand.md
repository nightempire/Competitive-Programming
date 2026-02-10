# 1859A_United_We_Stand

## Platform

Codeforces

## Problem Link

[A. United We Stand](https://codeforces.com/problemset/problem/1859/A)

## Problem Statement

You are given an array `a` of length `n` containing integers.

You must split the array into **two non-empty arrays** `b` and `c` such that:

* Every element of array `a` belongs to **exactly one** of `b` or `c`
* **All elements in `b` are equal**
* **Every element in `c` is strictly greater than the elements in `b`**

If it is **impossible** to create such arrays, print `-1`.
Otherwise, print the sizes and elements of arrays `b` and `c`.

## Input Format

* The first line contains an integer `t`, the number of test cases
* For each test case:

  * An integer `n`, the size of the array
  * `n` integers representing the array `a`

## Output Format

For each test case:

* If no valid split exists, print `-1`
* Otherwise:

  * Print two integers — the sizes of arrays `b` and `c`
  * Print the elements of array `b`
  * Print the elements of array `c`

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 100`
* `1 ≤ a[i] ≤ 100`

## Examples

### Example 1

Input

```
1
5
1 2 1 3 1
```

Explanation

* Minimum value = `1`
* Array `b` contains all `1`s → `[1, 1, 1]`
* Array `c` contains remaining values → `[2, 3]`
* Both arrays are non-empty and satisfy conditions

Output

```
3 2
1 1 1
2 3
```

---

### Example 2

Input

```
1
3
5 5 5
```

Explanation

* All elements are equal
* No element is strictly greater than the minimum
* Array `c` would be empty

Output

```
-1
```

## Approach

**Minimum Element Partitioning**

## Intuition

To satisfy the condition that:

* All elements of `b` are equal
* All elements of `c` are strictly greater than `b`

The most natural choice is:

* Let `b` contain **all occurrences of the minimum element**
* Let `c` contain **all remaining elements**

If there are **no elements greater than the minimum**, then such a split is impossible.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read `n`
  * Read the array and find the minimum value `mn`
  * Create two arrays:

    * `b` → elements equal to `mn`
    * `c` → elements greater than `mn`
  * If `c` is empty:

    * Print `-1`
  * Else:

    * Print sizes of `b` and `c`
    * Print elements of `b`
    * Print elements of `c`

## Visual Walkthrough

### Case 1: `1 2 1 3 1`

```
Minimum = 1
b = [1, 1, 1]
c = [2, 3]
Valid split
```

---

### Case 2: `4 4 4`

```
Minimum = 4
b = [4, 4, 4]
c = []
Invalid split
```

---

### Case 3: `2 3`

```
Minimum = 2
b = [2]
c = [3]
Valid split
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each element is processed a constant number of times.

### Space Complexity

**O(n)**

Additional vectors `b` and `c` are used to store the partitioned elements.

## Solution Explanation

The solution leverages a simple observation:

* The smallest value must define array `b`
* Any value equal to the minimum cannot be placed in `c`
* At least one element must be strictly greater than the minimum for a valid split

By grouping elements based on comparison with the minimum, the required arrays are constructed directly and efficiently.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int n;
        cin >> n;

        int a[n];
        int mn = INT_MAX;

        // Read array and find minimum
        for (int i = 0; i < n; i++) {
            cin >> a[i];
            if (a[i] < mn) mn = a[i];
        }

        vector<int> b, c;

        // Partition elements
        for (int x : a) {
            if (x == mn)
                b.push_back(x);
            else
                c.push_back(x);
        }

        // If no element is strictly greater than minimum
        if (c.empty()) {
            cout << "-1\n";
        } else {
            cout << b.size() << " " << c.size() << '\n';

            for (int x : b) cout << x << ' ';
            cout << '\n';

            for (int x : c) cout << x << ' ';
            cout << '\n';
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Input Array | b       | c     | Output |
| ----------- | ------- | ----- | ------ |
| `1 2 1 3 1` | `1 1 1` | `2 3` | Valid  |
| `5 5 5`     | `5 5 5` | —     | -1     |
| `2 3`       | `2`     | `3`   | Valid  |

## Edge Cases to Consider

* All elements equal
* Exactly one element greater than minimum
* Minimum appearing only once
* Multiple test cases

## Common Test Cases

* Arrays with duplicates
* Arrays with one distinct minimum
* Small-sized arrays

## Common Mistakes to Avoid

* Choosing an arbitrary value instead of the minimum
* Allowing `c` to be empty
* Printing arrays in incorrect order

## Interview Relevance

* Tests array partitioning logic
* Evaluates condition-based grouping
* Reinforces careful interpretation of constraints

## What This Problem Teaches

* Leveraging minimum values for partitioning
* Constructive problem-solving
* Validating feasibility before printing results

## Key Takeaways

* Minimum-based grouping simplifies constraints
* Always ensure both required groups are non-empty
* Simple observations can eliminate complex logic

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The solution relies on a clear observation and straightforward array processing, making it ideal for beginners and competitive programming warm-ups.