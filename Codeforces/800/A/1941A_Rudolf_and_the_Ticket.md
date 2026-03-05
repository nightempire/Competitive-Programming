# A_Rudolf_and_the_Ticket

## Platform

Codeforces

## Problem Link

[A. Rudolf and the Ticket](https://codeforces.com/problemset/problem/1941/A)

## Problem Statement

Rudolf wants to buy a ticket, but the ticket price depends on selecting two values from two different lists.

You are given two arrays:

* `b` containing `n` integers
* `c` containing `m` integers

You also have an integer `k`.

A pair `(i, j)` is considered **valid** if:

```
b[i] + c[j] ≤ k
```

Your task is to determine the **number of valid pairs** that satisfy this condition.

Each pair consists of:

* one element from array `b`
* one element from array `c`

For every test case, output the total number of valid pairs.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * The first line contains three integers `n`, `m`, and `k`.
  * The second line contains `n` integers representing array `b`.
  * The third line contains `m` integers representing array `c`.

## Output Format

For each test case, print a single integer — the number of valid pairs.

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n, m ≤ 100`
* `1 ≤ b[i], c[j] ≤ 100`
* `1 ≤ k ≤ 200`

## Examples

### Example 1

Input

```
1
3 3 7
1 2 3
2 3 4
```

Explanation

Check all combinations:

| b[i] | c[j] | Sum | Valid |
| ---- | ---- | --- | ----- |
| 1    | 2    | 3   | Yes   |
| 1    | 3    | 4   | Yes   |
| 1    | 4    | 5   | Yes   |
| 2    | 2    | 4   | Yes   |
| 2    | 3    | 5   | Yes   |
| 2    | 4    | 6   | Yes   |
| 3    | 2    | 5   | Yes   |
| 3    | 3    | 6   | Yes   |
| 3    | 4    | 7   | Yes   |

Total valid pairs = **9**

Output

```
9
```

---

### Example 2

Input

```
1
2 3 5
3 4
2 3 4
```

Explanation

| b[i] | c[j] | Sum | Valid |
| ---- | ---- | --- | ----- |
| 3    | 2    | 5   | Yes   |
| 3    | 3    | 6   | No    |
| 3    | 4    | 7   | No    |
| 4    | 2    | 6   | No    |
| 4    | 3    | 7   | No    |
| 4    | 4    | 8   | No    |

Total valid pairs = **1**

Output

```
1
```

---

### Example 3

Input

```
1
3 2 6
1 5 3
2 4
```

Explanation

| b[i] | c[j] | Sum | Valid |
| ---- | ---- | --- | ----- |
| 1    | 2    | 3   | Yes   |
| 1    | 4    | 5   | Yes   |
| 5    | 2    | 7   | No    |
| 5    | 4    | 9   | No    |
| 3    | 2    | 5   | Yes   |
| 3    | 4    | 7   | No    |

Total valid pairs = **3**

Output

```
3
```

## Approach

Brute Force Pair Enumeration (Nested Iteration)

## Intuition

The problem requires counting all pairs `(b[i], c[j])` whose sum does not exceed `k`.

Since:

* `n ≤ 100`
* `m ≤ 100`

The total possible pairs are:

```
n × m ≤ 10,000
```

This is small enough to check every pair directly.

Therefore:

* Iterate through every element in `b`
* For each element, iterate through every element in `c`
* Check whether their sum satisfies the condition

If it does, increment the counter.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read `n`, `m`, `k`.
  * Read array `b` of size `n`.
  * Read array `c` of size `m`.
  * Initialize `count = 0`.
  * For each element `i` in `b`:

    * For each element `j` in `c`:

      * If `i + j ≤ k`:

        * Increment `count`.
  * Print `count`.

## Visual Walkthrough

### Test Case 1

Input arrays:

```
b = [1, 2, 3]
c = [2, 3, 4]
k = 7
```

Pair checking:

```
1 + 2 = 3  ✓
1 + 3 = 4  ✓
1 + 4 = 5  ✓
2 + 2 = 4  ✓
2 + 3 = 5  ✓
2 + 4 = 6  ✓
3 + 2 = 5  ✓
3 + 3 = 6  ✓
3 + 4 = 7  ✓
```

Total valid pairs:

```
9
```

---

### Test Case 2

```
b = [3, 4]
c = [2, 3, 4]
k = 5
```

Pair results:

```
3 + 2 = 5  ✓
3 + 3 = 6  ✗
3 + 4 = 7  ✗
4 + 2 = 6  ✗
4 + 3 = 7  ✗
4 + 4 = 8  ✗
```

Valid pairs:

```
1
```

---

### Test Case 3

```
b = [1, 5, 3]
c = [2, 4]
k = 6
```

Pair results:

```
1 + 2 = 3 ✓
1 + 4 = 5 ✓
5 + 2 = 7 ✗
5 + 4 = 9 ✗
3 + 2 = 5 ✓
3 + 4 = 7 ✗
```

Total valid pairs:

```
3
```

## Complexity Analysis

### Time Complexity

O(n × m)

For each element in array `b`, we iterate through all elements in array `c`.

Maximum operations per test case:

```
100 × 100 = 10,000
```

Which is efficient.

### Space Complexity

O(n + m)

Space is used only to store the two arrays.

## Solution Explanation

The program reads the two arrays and checks all possible pairs.

Using nested loops, it calculates the sum of each pair and verifies whether it satisfies the condition `≤ k`.

Whenever the condition holds true, the counter increases.

After all pairs are evaluated, the final count is printed.

This direct enumeration approach works efficiently due to the small constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Sizes of the arrays and maximum allowed sum
        int n, m, k;

        cin >> n >> m >> k;

        // Arrays storing ticket values
        vector<int> b(n), c(m);

        // Read array b
        for (int i = 0; i < n; i++)
            cin >> b[i];

        // Read array c
        for (int i = 0; i < m; i++)
            cin >> c[i];

        // Counter for valid pairs
        int count = 0;

        // Check all possible pairs
        for (int i : b) {

            // Iterate through second array
            for (int j : c) {

                // If sum of pair is within limit
                if (i + j <= k) {

                    // Increase valid pair count
                    count++;
                }
            }
        }

        // Print the result
        cout << count << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n | m | k | Array b | Array c | Valid Pairs |
| - | - | - | ------- | ------- | ----------- |
| 3 | 3 | 7 | 1 2 3   | 2 3 4   | 9           |
| 2 | 3 | 5 | 3 4     | 2 3 4   | 1           |
| 3 | 2 | 6 | 1 5 3   | 2 4     | 3           |

## Edge Cases to Consider

* `n = 1` or `m = 1`
* All sums exceed `k`
* All pairs satisfy the condition
* Minimum values in arrays
* Maximum values in arrays

## Common Test Cases

* Arrays containing identical numbers
* `k` equal to the smallest possible sum
* `k` greater than all possible sums
* Small arrays with multiple test cases

## Common Mistakes to Avoid

* Forgetting to reset the counter for each test case
* Incorrect nested loop boundaries
* Using `< k` instead of `≤ k`

## Interview Relevance

* Demonstrates nested iteration patterns
* Tests ability to count pair combinations
* Introduces basic constraint-based pair filtering

## What This Problem Teaches

* Efficient pair enumeration
* Handling multiple test cases
* Applying condition checks across combinations

## Key Takeaways

* When constraints are small, brute force can be optimal
* Always analyze maximum pair combinations
* Clean nested loops simplify implementation

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It primarily tests nested iteration and condition checking, making it a beginner-friendly problem commonly encountered in early competitive programming practice.