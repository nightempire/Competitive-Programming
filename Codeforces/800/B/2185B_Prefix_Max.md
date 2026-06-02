## 2185B. Prefix Max

## Platform

Codeforces

## Problem Link

[B. Prefix Max](https://codeforces.com/problemset/problem/2185/B)

## Problem Statement

You are given an array of `n` integers.

The task is to determine the maximum possible value of the sum of prefix maximums after performing the operations described in the problem.

A **prefix maximum** for position `i` is defined as:

```text
max(a1, a2, ..., ai)
```

For each test case, output the required maximum value.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`.
  * The second line contains `n` integers.

## Output Format

* For each test case, print a single integer — the maximum possible answer.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 2 × 10^5`
* `1 ≤ a[i] ≤ 10^9`
* Sum of `n` over all test cases does not exceed `2 × 10^5`

## Examples

### Example 1

Input

```text
1
5
1 3 2 5 4
```

Explanation

Maximum element:

```text
5
```

Optimal answer:

```text
5 × 5 = 25
```

Output

```text
25
```

---

### Example 2

Input

```text
1
4
7 7 7 7
```

Explanation

Maximum element:

```text
7
```

Answer:

```text
4 × 7 = 28
```

Output

```text
28
```

---

### Example 3

Input

```text
1
3
2 8 5
```

Explanation

Maximum element:

```text
8
```

Answer:

```text
3 × 8 = 24
```

Output

```text
24
```

## Approach

Greedy Observation (Maximum Element)

## Intuition

The provided solution reveals an important observation:

* Only the maximum element of the array matters.
* Let:

```text
maxi = maximum element in the array
```

The answer becomes:

```text
n × maxi
```

Therefore, we simply need to find the largest value in the array and multiply it by the array size.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read `n`.

  * Initialize `maxi = 1`.

  * Traverse all elements:

    * Update `maxi` whenever a larger element is found.

  * Compute:

    ```text
    answer = n × maxi
    ```

  * Print the answer.

## Visual Walkthrough

### Case 1

```text
Array = [1, 3, 2, 5, 4]
```

Finding maximum:

```text
1 → 3 → 3 → 5 → 5
```

Maximum element:

```text
5
```

Answer:

```text
5 × 5 = 25
```

---

### Case 2

```text
Array = [7, 7, 7, 7]
```

Maximum:

```text
7
```

Answer:

```text
4 × 7 = 28
```

---

### Case 3

```text
Array = [2, 8, 5]
```

Maximum:

```text
8
```

Answer:

```text
3 × 8 = 24
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

The array is scanned exactly once to find the maximum element.

### Space Complexity

**O(1)**

Only a few variables are used regardless of input size.

## Solution Explanation

The solution maintains a variable `maxi` that stores the largest value encountered while reading the array.

After all elements are processed:

```text
maxi = largest element
```

The final answer is:

```text
n × maxi
```

This avoids any additional processing and produces the result in linear time.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Size of array
        int n;
        cin >> n;

        // Current number and maximum element
        int num, maxi = 1;

        // Read array and find maximum element
        for(int i = 0; i < n; i++) {

            cin >> num;

            if(num > maxi) {
                maxi = num;
            }
        }

        // Print final answer
        cout << n * maxi << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Array       | Maximum Element | n | Output |
| ----------- | --------------- | - | ------ |
| [1,3,2,5,4] | 5               | 5 | 25     |
| [7,7,7,7]   | 7               | 4 | 28     |
| [2,8,5]     | 8               | 3 | 24     |
| [10]        | 10              | 1 | 10     |
| [4,1,9,2,6] | 9               | 5 | 45     |

## Edge Cases to Consider

* Array of size `1`
* All elements equal
* Maximum element at the beginning
* Maximum element at the end
* Very large element values

## Common Test Cases

* Strictly increasing array
* Strictly decreasing array
* Uniform array
* Random unordered array
* Single-element array

## Common Mistakes to Avoid

* Forgetting to update the maximum element correctly.
* Initializing the maximum value improperly.
* Multiplying by an incorrect count instead of `n`.

## Interview Relevance

* Tests basic array traversal.
* Reinforces maximum element search.
* Demonstrates optimization through observations.

## What This Problem Teaches

* Efficient single-pass processing.
* Finding extrema in an array.
* Leveraging problem observations to simplify computation.

## Key Takeaways

* Often only one critical value (the maximum) determines the answer.
* A single traversal can solve many array problems efficiently.
* Always look for mathematical simplifications before attempting complex solutions.

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The implementation is straightforward once the observation is made that the answer depends solely on the maximum element of the array. The solution requires only a linear scan and constant extra space.