# A. Spy Detected!

## Platform

Codeforces

## Problem Link

[A. Spy Detected!](https://codeforces.com/problemset/problem/1512/A)

## Problem Statement

You are given an array of integers for each test case.

* All elements in the array are **equal**, except **one element**.
* This unique element is the **spy**.

Your task is to find and print the **1-based index** of the spy element.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * An integer `n`, the size of the array
  * A line containing `n` integers

```
n
a1 a2 a3 ... an
```

## Output Format

For each test case, print the **index (1-based)** of the element that is different from the others.

## Constraints

* `1 ≤ t ≤ 1000`
* `3 ≤ n ≤ 100`
* Exactly one element differs from the rest

## Examples

### Example 1

Input

```
2
4
1 1 2 1
3
5 7 7
```

Explanation

* Test case 1: `2` is different → index `3`
* Test case 2: `5` is different → index `1`

Output

```
3
1
```

## Approach

**Local Comparison of Adjacent Elements**

## Intuition

Since all elements are equal except one, the spy can be identified by comparing **just the first few elements**.

Observations:

* If `nums[i] != nums[i+1]`, one of them is the spy
* Comparing with another element (like the last one) resolves which one is unique
* Only the first three elements are sufficient to detect the spy

This avoids counting frequencies or using extra memory.

## Algorithm Steps

* Read the number of test cases
* For each test case:

  * Read `n` and the array
  * Iterate from index `0` to `n-3`
  * Compare `nums[i]`, `nums[i+1]`, and `nums[i+2]`
  * Determine which one differs
  * Print its **1-based index**

## Visual Walkthrough

Array:

```
[1, 1, 2, 1]
```

Comparison:

```
nums[0] == nums[1]
nums[1] != nums[2]
```

Spy is `nums[2]` → index `3`

Another example:

```
[5, 7, 7]
```

Comparison:

```
nums[0] != nums[1]
nums[0] != nums[2]
```

Spy is `nums[0]` → index `1`

## Complexity Analysis

### Time Complexity

O(n)

Each test case scans the array once.

### Space Complexity

O(1)

No additional data structures are used.

## Solution Explanation

The solution checks differences between adjacent elements to identify the unique value.

When a mismatch is found:

* The element that differs from the majority is identified by comparing with a third element
* Its index is immediately printed

This approach is efficient, concise, and optimal for the given constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while (t--) {

        // Size of the array
        int n;
        cin >> n;

        // Read the array
        int nums[n];
        for (int i = 0; i < n; i++) {
            cin >> nums[i];
        }

        // Iterate to find the unique element
        for (int i = 0; i < n - 2; i++) {

            // If current and next elements differ
            if (nums[i] != nums[i + 1]) {

                // Compare with the last element to identify the spy
                if (nums[i] != nums[n - 1]) {
                    cout << i + 1;   // nums[i] is the spy
                } else {
                    cout << i + 2;   // nums[i + 1] is the spy
                }
                break;
            }

            // If the third element differs
            else if (nums[i + 1] != nums[i + 2]) {
                cout << i + 3;       // nums[i + 2] is the spy
                break;
            }
        }

        // New line after each test case
        cout << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Array        | Spy Value | Index |
| ------------ | --------- | ----- |
| [1, 1, 2, 1] | 2         | 3     |
| [7, 5, 7]    | 5         | 2     |
| [9, 3, 3, 3] | 9         | 1     |
| [4, 4, 4, 2] | 2         | 4     |

## Edge Cases to Consider

* Spy at the beginning
* Spy at the end
* Minimal array size (`n = 3`)

## Common Test Cases

* All equal except first
* All equal except middle
* All equal except last

## Common Mistakes to Avoid

* Using frequency maps unnecessarily
* Forgetting 1-based indexing
* Overcomplicating with sorting

## Interview Relevance

* Tests logical reasoning
* Emphasizes pattern recognition
* Shows how to reduce problem scope efficiently

## What This Problem Teaches

* Leveraging constraints to simplify logic
* Using minimal comparisons
* Writing efficient conditional checks

## Key Takeaways

* One unique element can be detected locally
* No need for extra memory or full scans
* Clear logic leads to concise solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on observation and efficient comparison rather than complex data structures, making it ideal for beginners and competitive programming practice.