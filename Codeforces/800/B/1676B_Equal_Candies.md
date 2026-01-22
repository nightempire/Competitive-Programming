# B_Equal_Candies

## Platform

Codeforces

## Problem Link

[B. Equal Candies](https://codeforces.com/problemset/problem/1676/B)

## Problem Statement

You are given several test cases.
In each test case, there are `n` boxes, where each box contains some number of candies.

In one operation, you are allowed to **remove exactly one candy from any box**.

Your objective is to make the number of candies in **all boxes equal** using the **minimum number of operations**.

You must compute and output the minimum number of candies that need to be removed.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`, the number of boxes.
  * The second line contains `n` integers representing the number of candies in each box.

## Output Format

For each test case, output a single integer — the minimum number of candies to remove so that all boxes contain the same number of candies.

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 50`
* `1 ≤ candies[i] ≤ 100`
* Sum of `n` over all test cases is small enough to allow direct iteration

## Examples

### Example 1

Input

```
2
3
1 2 3
4
5 5 5 5
```

Explanation

* Test case 1:

  * Minimum candies in a box = 1
  * Remove `(2−1) + (3−1) = 3` candies
* Test case 2:

  * All boxes already have equal candies
  * No removals needed

Output

```
3
0
```

### Example 2

Input

```
1
5
4 1 6 2 3
```

Explanation

* Minimum candies = 1
* Total removals = `(4−1) + (6−1) + (2−1) + (3−1) = 11`

Output

```
11
```

## Approach

**Greedy – Minimum Normalization Strategy**

The solution uses a greedy approach by reducing all boxes to the minimum candy count present.

## Intuition

Since only **removals** are allowed:

* Increasing candy count is impossible
* The only feasible target value is the **minimum number of candies among all boxes**

Reducing every box to this minimum guarantees:

* All boxes become equal
* The total number of removals is minimized

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read `n`.
  * Read the candies in all boxes.
  * Find the minimum candy count `mini`.
  * For each box:

    * Add `(candies − mini)` to the total operations.
* Output the total number of operations.

## Visual Walkthrough

### Test Case 1

Input

```
1 2 3
```

Minimum value:

```
mini = 1
```

Operations:

```
Box 1: 1 → 1 (0 removals)
Box 2: 2 → 1 (1 removal)
Box 3: 3 → 1 (2 removals)
```

Total removals:

```
0 + 1 + 2 = 3
```

---

### Test Case 2

Input

```
4 1 6 2 3
```

Minimum value:

```
mini = 1
```

Operations:

```
(4−1) + (6−1) + (2−1) + (3−1) = 11
```

---

### Test Case 3

Input

```
5 5 5
```

Minimum value:

```
mini = 5
```

No removals required → `0`

## Complexity Analysis

### Time Complexity

**O(n) per test case**

* One pass to find the minimum
* One pass to calculate total removals

### Space Complexity

**O(n)**

* The array storing candy counts is proportional to `n`

## Solution Explanation

The solution identifies the smallest candy count and treats it as the target value.
Every other box is reduced to this value by removing extra candies.
This guarantees correctness because removing fewer candies is impossible, and removing more would be unnecessary.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <climits>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Number of boxes
        int n;
        cin >> n;

        // Array to store candies in each box
        int boxes[n];

        // Variable to track minimum candies
        int mini = INT_MAX;

        // Read candy counts and find minimum
        for (int i = 0; i < n; i++) {
            cin >> boxes[i];
            if (boxes[i] < mini) {
                mini = boxes[i];
            }
        }

        // Total number of candies to remove
        int total = 0;

        // Calculate removals required
        for (int candies : boxes) {
            total += (candies - mini);
        }

        // Output the result
        cout << total << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Input Boxes | Minimum | Total Removals |
| --------- | ----------- | ------- | -------------- |
| 1         | 1 2 3       | 1       | 3              |
| 2         | 5 5 5 5     | 5       | 0              |
| 3         | 4 1 6 2 3   | 1       | 11             |
| 4         | 10 9        | 9       | 1              |
| 5         | 7           | 7       | 0              |

## Edge Cases to Consider

* Only one box
* All boxes already equal
* Large difference between maximum and minimum
* Multiple boxes sharing the minimum value

## Common Test Cases

* Uniform candy distribution
* One box significantly larger than others
* Random distribution of candies

## Common Mistakes to Avoid

* Trying to average values instead of using the minimum
* Forgetting that only removal operations are allowed
* Miscounting operations by including the minimum box

## Interview Relevance

* Demonstrates greedy problem-solving
* Tests ability to reason about constraints
* Reinforces minimization strategies

## What This Problem Teaches

* Greedy choice based on constraints
* Importance of selecting the correct target state
* Translating problem restrictions into optimal logic

## Key Takeaways

* When only removals are allowed, the minimum value is the optimal target
* Greedy strategies can yield optimal results when justified
* Simple logic often leads to clean and efficient solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic greedy reasoning and array traversal, making it ideal for beginners and technical interview preparation.