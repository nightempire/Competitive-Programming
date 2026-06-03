## 2149A. Be Positive

## Platform

Codeforces

## Problem Link

[A. Be Positive](https://codeforces.com/problemset/problem/2149/A)

## Problem Statement

You are given an array consisting only of the values:

```text
-1, 0, 1
```

In one operation, you may change an element's value according to the rules specified in the problem.

Your task is to determine the **minimum number of operations** required so that:

* The product of all elements becomes positive.
* The sum of all elements becomes non-negative.

For each test case, output the minimum number of operations needed.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`.
  * The second line contains `n` integers, each belonging to `{ -1, 0, 1 }`.

## Output Format

* For each test case, print a single integer — the minimum number of operations required.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 100`
* `a[i] ∈ { -1, 0, 1 }`

## Examples

### Example 1

Input

```text
3
3
-1 -1 1
4
-1 0 1 1
2
0 0
```

Explanation

#### Test Case 1

```text
Negative count = 2 (even)
Zero count = 0
```

Product is already positive.

Operations needed:

```text
0
```

Output

```text
0
```

---

#### Test Case 2

```text
Negative count = 1 (odd)
Zero count = 1
```

Convert one zero to one:

```text
Operations = 1
```

Output

```text
1
```

---

#### Test Case 3

```text
Negative count = 0
Zero count = 2
```

Convert both zeros appropriately.

Output

```text
2
```

## Approach

Greedy Counting / Parity Observation

## Intuition

The provided solution only tracks:

* Number of zeros (`z`)
* Parity of the count of `-1`s (`neg`)

Key observations:

### Zeros

Every zero must eventually be converted, contributing:

```text
z operations
```

### Negative Ones

If the count of `-1` values is odd:

```text
(-1) × (-1) × ... × (-1)
```

produces a negative product.

To make the product positive, two additional operations are required.

Thus:

```text
answer = zeros + 2 (if negatives count is odd)
answer = zeros     (if negatives count is even)
```

The code efficiently tracks only the parity of negative values instead of counting them completely.

## Algorithm Steps

* Read `t`.
* For each test case:

  * Initialize:

    ```text
    z = 0
    neg = false
    ```
  * Traverse the array.

    * If element is `0`:

      ```text
      z++
      ```

    * If element is `-1`:

      ```text
      neg = !neg
      ```

      This keeps track of odd/even parity.
  * Compute:

    ```text
    answer = z + (neg ? 2 : 0)
    ```
  * Print the answer.

## Visual Walkthrough

### Case 1

```text
Array = [-1, -1, 1]
```

Processing:

```text
z = 0

neg:
false → true → false
```

Final:

```text
z = 0
neg = false
```

Answer:

```text
0
```

---

### Case 2

```text
Array = [-1, 0, 1, 1]
```

Processing:

```text
z = 1

neg:
false → true
```

Final:

```text
z = 1
neg = true
```

Answer:

```text
1 + 2 = 3
```

---

### Case 3

```text
Array = [0, 0]
```

Processing:

```text
z = 2
neg = false
```

Answer:

```text
2
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each element is processed exactly once.

### Space Complexity

**O(1)**

Only two variables are maintained regardless of input size.

## Solution Explanation

The solution does not need the exact count of negative values—only whether that count is odd or even.

A boolean variable `neg` is toggled whenever `-1` is encountered:

```cpp
neg = !neg;
```

After processing:

* `z` stores the number of zeros.
* `neg` indicates whether the number of negative values is odd.

The final answer is:

```text
zeros + 2 (if odd negatives)
```

which is implemented as:

```cpp
z + neg * 2
```

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

        // Number of elements
        int n;

        // Count of zeros
        int z = 0;

        cin >> n;

        // Tracks parity of negative ones
        bool neg = false;

        while(n--) {

            int num;
            cin >> num;

            // Count zeros
            if(num == 0) {
                z++;
            }

            // Toggle parity for every -1
            else if(num == -1) {
                neg = !neg;
            }
        }

        // Answer:
        // zeros + 2 if count(-1) is odd
        cout << z + neg * 2 << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Array      | Zero Count | Negative Parity | Output |
| ---------- | ---------- | --------------- | ------ |
| [-1,-1,1]  | 0          | Even            | 0      |
| [-1,0,1,1] | 1          | Odd             | 3      |
| [0,0]      | 2          | Even            | 2      |
| [-1]       | 0          | Odd             | 2      |
| [1,1,1]    | 0          | Even            | 0      |

## Edge Cases to Consider

* All elements are `0`.
* All elements are `1`.
* Single element `-1`.
* Odd number of negative values.
* Even number of negative values.
* Mixture of `-1`, `0`, and `1`.

## Common Test Cases

* `[-1, -1]`
* `[-1, 0]`
* `[0, 0, 0]`
* `[1, 1, 1]`
* `[-1, -1, 0, 1]`

## Common Mistakes to Avoid

* Counting negative values instead of tracking parity.
* Forgetting to account for zeros separately.
* Adding only `1` instead of `2` when the negative count is odd.

## Interview Relevance

* Tests parity-based reasoning.
* Demonstrates optimization through state compression.
* Reinforces greedy counting techniques.

## What This Problem Teaches

* Tracking parity efficiently using a boolean.
* Simplifying problems through observations.
* Using counts instead of simulation.

## Key Takeaways

* Sometimes only parity matters, not the exact count.
* Boolean toggling is an elegant way to track odd/even occurrences.
* Greedy counting often leads to very concise solutions.

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The implementation is short, but the main challenge is identifying that only the parity of negative values and the number of zeros affect the answer. Once this observation is made, the solution becomes straightforward.