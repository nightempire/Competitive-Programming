# B_Gifts_Fixing

## Platform

Codeforces

## Problem Link

[B. Gifts Fixing](https://codeforces.com/problemset/problem/1399/B)

## Problem Statement

You are given two arrays:

* `a` representing the number of **candies**
* `b` representing the number of **oranges**

Both arrays have length `n`.

For each index `i`, you have a pair `(a[i], b[i])`.

You can perform the following operation any number of times:

* Decrease `a[i]` by `1`
* Decrease `b[i]` by `1`
* Or decrease **both simultaneously** by `1`

However, values cannot become negative.

Your goal is to make the arrays **equal to their minimum possible values** such that:

```text
a[i] = min(a)
b[i] = min(b)
```

for every index `i`.

Determine the **minimum number of operations required** to achieve this.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * The first line contains an integer `n`.
  * The second line contains `n` integers representing array `a`.
  * The third line contains `n` integers representing array `b`.

## Output Format

For each test case, print a single integer — the **minimum number of operations required**.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 50`
* `0 ≤ a[i], b[i] ≤ 10^9`

## Examples

### Example 1

Input

```
1
3
3 5 6
3 2 3
```

Explanation

Minimum values:

```
min(a) = 3
min(b) = 2
```

Required reductions:

| Index | a[i] → | b[i] → |
| ----- | ------ | ------ |
| 1     | 3 → 3  | 3 → 2  |
| 2     | 5 → 3  | 2 → 2  |
| 3     | 6 → 3  | 3 → 2  |

Operations per index:

| Index | Candy Decrease | Orange Decrease | Operations |
| ----- | -------------- | --------------- | ---------- |
| 1     | 0              | 1               | 1          |
| 2     | 2              | 0               | 2          |
| 3     | 3              | 1               | 3          |

Total operations:

```
1 + 2 + 3 = 6
```

Output

```
6
```

---

### Example 2

Input

```
1
2
1 2
2 1
```

Explanation

Minimum values:

```
min(a) = 1
min(b) = 1
```

Reductions:

| Index | Candy | Orange | Operations |
| ----- | ----- | ------ | ---------- |
| 1     | 0     | 1      | 1          |
| 2     | 1     | 0      | 1          |

Total:

```
2
```

Output

```
2
```

---

### Example 3

Input

```
1
4
4 4 4 4
4 4 4 4
```

Explanation

Both arrays already equal their minimum values.

Operations required:

```
0
```

Output

```
0
```

## Approach

Greedy Reduction with Minimum Baseline

## Intuition

Each pair `(a[i], b[i])` must be reduced to:

```
(minA, minB)
```

Where:

```
minA = minimum value in array a
minB = minimum value in array b
```

For each index `i`:

```
da = a[i] - minA
db = b[i] - minB
```

Since we can decrease **both simultaneously**, the optimal strategy is:

```
operations = max(da, db)
```

Why?

* When decreasing both simultaneously, both values reduce together.
* After one reaches its minimum, we continue decreasing the other individually.

Thus the number of steps required is governed by the **larger reduction needed**.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read `n`.
  * Read array `a`.
  * Read array `b`.
  * Find `minA` and `minB`.
  * Initialize `operations = 0`.
  * For each index `i`:

    * Compute:

      ```
      da = a[i] - minA
      db = b[i] - minB
      ```
    * Add `max(da, db)` to the total operations.
  * Print the total operations.

## Visual Walkthrough

### Test Case 1

Arrays:

```
a = [3,5,6]
b = [3,2,3]
```

Minimum values:

```
minA = 3
minB = 2
```

Differences:

| Index | da | db | Operations |
| ----- | -- | -- | ---------- |
| 1     | 0  | 1  | 1          |
| 2     | 2  | 0  | 2          |
| 3     | 3  | 1  | 3          |

Total:

```
6
```

---

### Test Case 2

```
a = [1,2]
b = [2,1]
```

Minimums:

```
minA = 1
minB = 1
```

Differences:

| Index | da | db | Operations |
| ----- | -- | -- | ---------- |
| 1     | 0  | 1  | 1          |
| 2     | 1  | 0  | 1          |

Total:

```
2
```

---

### Test Case 3

```
a = [4,4,4,4]
b = [4,4,4,4]
```

Minimums:

```
minA = 4
minB = 4
```

Differences:

```
All zero → operations = 0
```

## Complexity Analysis

### Time Complexity

O(n) per test case.

* Finding minimum values requires `O(n)`.
* Calculating operations also requires `O(n)`.

### Space Complexity

O(n)

Arrays store `n` elements each.

## Solution Explanation

The algorithm first identifies the **smallest value in each array**.

These represent the target values.

For every index:

* Calculate how much the candy count must decrease.
* Calculate how much the orange count must decrease.

Since a single operation can reduce both simultaneously, the number of operations needed equals the **maximum of these two reductions**.

Summing this for all indices yields the minimal total operations.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <algorithm>
#include <climits>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while (t--) {

        // Number of gift pairs
        int n;
        cin >> n;

        // 2D array:
        // nums[0] → candies
        // nums[1] → oranges
        int nums[2][n];

        // Minimum values for candies and oranges
        int mn[2] = {INT_MAX, INT_MAX};

        // Read candies array and compute minimum
        for (int i = 0; i < n; i++) {
            cin >> nums[0][i];

            if (nums[0][i] < mn[0])
                mn[0] = nums[0][i];
        }

        // Read oranges array and compute minimum
        for (int i = 0; i < n; i++) {
            cin >> nums[1][i];

            if (nums[1][i] < mn[1])
                mn[1] = nums[1][i];
        }

        // Total number of operations
        long long count = 0;

        // Calculate operations needed for each index
        for (int i = 0; i < n; i++) {

            // Required reductions
            int da = nums[0][i] - mn[0];
            int db = nums[1][i] - mn[1];

            // Optimal operations = maximum reduction
            count += max(da, db);
        }

        // Print result
        cout << count << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| a     | b     | minA | minB | Result |
| ----- | ----- | ---- | ---- | ------ |
| 3 5 6 | 3 2 3 | 3    | 2    | 6      |
| 1 2   | 2 1   | 1    | 1    | 2      |
| 4 4 4 | 4 4 4 | 4    | 4    | 0      |

## Edge Cases to Consider

* Arrays already at minimum values
* One array requires reduction while the other does not
* Large numbers (`10^9`)
* Single element arrays (`n = 1`)

## Common Test Cases

* Identical arrays
* Highly unbalanced values
* Large differences between elements
* Minimum constraint values

## Common Mistakes to Avoid

* Reducing arrays independently instead of simultaneously when possible
* Forgetting to compute minimum values first
* Using `min(da, db)` instead of `max(da, db)`

## Interview Relevance

* Demonstrates greedy optimization
* Tests ability to minimize operations
* Introduces efficient problem reduction strategies

## What This Problem Teaches

* Leveraging simultaneous operations
* Mathematical simplification of operations
* Greedy strategy design

## Key Takeaways

* Reducing both values simultaneously minimizes operations
* Always analyze if combined operations are possible
* Greedy solutions often arise from simple mathematical insights

## Problem Difficulty Analysis

This is an **Easy-to-Medium level** problem.

While the implementation is simple, recognizing the greedy observation that **`max(da, db)` determines the optimal number of operations** is the key insight.