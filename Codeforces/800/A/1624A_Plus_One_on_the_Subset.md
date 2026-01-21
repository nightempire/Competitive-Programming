# A_Plus_One_on_the_Subset

## Platform

Codeforces

## Problem Link

[A. Plus One on the Subset](https://codeforces.com/problemset/problem/1624/A)

## Problem Statement

You are given an array of integers.

In one operation, you may choose **any non-empty subset** of the array and increase **each element of that subset by 1**.

Your task is to determine the **minimum number of operations** required to make **all elements of the array equal**.

This process must be evaluated independently for multiple test cases.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * An integer `n`, the size of the array
  * A line containing `n` integers representing the array elements

## Output Format

For each test case, print a single integer representing the minimum number of operations required.

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 50`
* `0 ≤ array[i] ≤ 10^9`

## Examples

### Example 1

Input

```
3
3
1 2 3
4
5 5 5 5
5
1 1 1 10 1
```

Explanation

* Test case 1:

  * Minimum = 1, Maximum = 3
  * Operations needed = `3 - 1 = 2`
* Test case 2:

  * All elements already equal
  * Operations needed = `0`
* Test case 3:

  * Minimum = 1, Maximum = 10
  * Operations needed = `10 - 1 = 9`

Output

```
2
0
9
```

### Example 2

Input

```
1
2
0 100
```

Explanation

* Minimum = 0, Maximum = 100
* Operations needed = `100`

Output

```
100
```

## Approach

**Greedy Observation Using Range Difference**

## Intuition

In a single operation, we can increment **any subset** of elements by 1.
This means:

* We can selectively increase smaller elements
* Larger elements do not need to be decreased

To make all elements equal with the minimum number of operations, the best strategy is to:

* Bring all elements up to the value of the **maximum element**

Each operation increases the difference between the minimum and maximum by exactly 1 for the chosen elements.

Therefore, the minimum number of operations required is simply:

```
maximum value − minimum value
```

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read the size of the array `n`
  * Initialize variables to track the minimum and maximum values
  * Traverse the array:

    * Update the minimum and maximum values
  * Compute the answer as:

    ```
    max − min
    ```
  * Output the result

## Visual Walkthrough

### Test Case 1

Array:

```
[1, 2, 3]
```

Minimum and maximum:

```
min = 1
max = 3
```

Operations:

```
Increase subset {1} twice → [3, 2, 3]
Increase subset {2} once  → [3, 3, 3]
```

Minimum operations:

```
3 − 1 = 2
```

---

### Test Case 2

Array:

```
[5, 5, 5, 5]
```

Minimum and maximum:

```
min = max = 5
```

Operations needed:

```
0
```

---

### Test Case 3

Array:

```
[1, 1, 1, 10, 1]
```

Minimum and maximum:

```
min = 1
max = 10
```

Operations needed:

```
10 − 1 = 9
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each element is scanned once to determine the minimum and maximum.

### Space Complexity

**O(1)**

Only constant extra variables are used.

## Solution Explanation

The solution relies on a key observation: because we can increment any subset in one operation, we only need to consider how far the smallest value is from the largest. Incrementing smaller values until they match the maximum yields the minimum number of steps. No simulation of operations is required, making the solution optimal and efficient.

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

    // Process each test case independently
    while (t--) {

        // Size of the array
        int n;
        cin >> n;

        // Variables to track maximum and minimum values
        int maximumValue = 0;
        int minimumValue = INT_MAX;

        // Read array elements and update min/max
        for (int i = 0; i < n; i++) {
            int num;
            cin >> num;

            // Update maximum element
            if (num > maximumValue) {
                maximumValue = num;
            }

            // Update minimum element
            if (num < minimumValue) {
                minimumValue = num;
            }
        }

        // Minimum operations required to make all elements equal
        int result = maximumValue - minimumValue;

        // Output the result
        cout << result << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input Array    | Minimum | Maximum | Output |
| -------------- | ------- | ------- | ------ |
| `[1, 2, 3]`    | 1       | 3       | 2      |
| `[5, 5, 5, 5]` | 5       | 5       | 0      |
| `[0, 100]`     | 0       | 100     | 100    |
| `[7]`          | 7       | 7       | 0      |

## Edge Cases to Consider

* Single-element arrays
* Arrays with all equal values
* Very large element values
* Large number of test cases

## Common Test Cases

* Strictly increasing arrays
* Strictly decreasing arrays
* Arrays with repeated minimum or maximum values

## Common Mistakes to Avoid

* Attempting to simulate each operation
* Forgetting that subsets can be chosen arbitrarily
* Overcomplicating a simple greedy observation

## Interview Relevance

* Tests ability to derive logic from constraints
* Evaluates understanding of greedy strategies
* Common problem to assess mathematical reasoning

## What This Problem Teaches

* Leveraging problem constraints to simplify solutions
* Recognizing when simulation is unnecessary
* Using min-max properties effectively

## Key Takeaways

* Subset operations allow selective incrementing
* The difference between max and min dictates the answer
* Simple observations often lead to optimal solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on observation and greedy reasoning rather than complex algorithms, making it suitable for beginners and interview warm-up practice.