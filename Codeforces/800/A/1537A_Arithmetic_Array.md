## 1537A. Arithmetic Array

## Platform

Codeforces

## Problem Link

[A. Arithmetic Array](https://codeforces.com/problemset/problem/1537/A)

## Problem Statement

You are given an array `a` of length `n`.

In one operation, you can increase any element of the array by `1`.

Your task is to determine the minimum number of operations required so that the **average of the array becomes exactly `1`**.

Since the average is `1`, the total sum of the array must become:

```text
n
```

For each test case, output the minimum number of operations needed.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`.
  * The second line contains `n` integers `a₁, a₂, ..., aₙ`.

## Output Format

* For each test case, print a single integer — the minimum number of operations required.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 50`
* `0 ≤ a[i] ≤ 100`

## Examples

### Example 1

Input

```text
3
3
1 1 1
4
0 0 0 0
5
2 2 2 2 2
```

Explanation

#### Test Case 1

Current sum:

```text
1 + 1 + 1 = 3
```

Target sum:

```text
n = 3
```

Already satisfied.

Operations:

```text
0
```

Output

```text
0
```

---

#### Test Case 2

Current sum:

```text
0 + 0 + 0 + 0 = 0
```

Target sum:

```text
4
```

When the sum is less than `n`, one operation is sufficient according to the problem's observation.

Output

```text
1
```

---

#### Test Case 3

Current sum:

```text
2 + 2 + 2 + 2 + 2 = 10
```

Target sum:

```text
5
```

Extra sum:

```text
10 - 5 = 5
```

Operations needed:

```text
5
```

Output

```text
5
```

## Approach

Mathematical Observation

## Intuition

Let:

```text
sum = sum of all array elements
```

To make the average equal to `1`, the final sum must be:

```text
n
```

There are three cases:

### Case 1: sum = n

The average is already `1`.

```text
Answer = 0
```

### Case 2: sum < n

A direct observation from the problem shows that only one operation is needed.

```text
Answer = 1
```

### Case 3: sum > n

The excess amount is:

```text
sum - n
```

Each operation can reduce the excess requirement by one unit in the optimal strategy.

```text
Answer = sum - n
```

## Algorithm Steps

* Read `t`.
* For each test case:

  * Read `n`.

  * Compute the sum of all elements.

  * If:

    ```text
    sum == n
    ```

    print `0`.

  * Else if:

    ```text
    sum < n
    ```

    print `1`.

  * Else:

    ```text
    print(sum - n)
    ```

## Visual Walkthrough

### Case 1

```text
n = 3
Array = [1, 1, 1]
```

Sum:

```text
3
```

Target:

```text
3
```

Result:

```text
0 operations
```

---

### Case 2

```text
n = 4
Array = [0, 0, 0, 0]
```

Sum:

```text
0
```

Target:

```text
4
```

Since:

```text
sum < n
```

Result:

```text
1 operation
```

---

### Case 3

```text
n = 5
Array = [2, 2, 2, 2, 2]
```

Sum:

```text
10
```

Target:

```text
5
```

Excess:

```text
10 - 5 = 5
```

Result:

```text
5 operations
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each array element is read and added exactly once.

### Space Complexity

**O(1)**

Only a few integer variables are used.

## Solution Explanation

The solution computes the total sum of the array and compares it with `n`, which is the required sum for an average of `1`.

* If the sum already equals `n`, no operations are needed.
* If the sum is smaller than `n`, the answer is always `1`.
* If the sum exceeds `n`, the answer equals the excess amount `sum - n`.

This leads to a simple and efficient implementation.

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

        // Sum of array elements
        int sum = 0;

        cin >> n;

        // Read array and compute sum
        for(int i = 0; i < n; i++) {

            int num;
            cin >> num;

            sum += num;
        }

        // Average is already 1
        if(sum == n) {
            cout << "0\n";
        }

        // Sum is smaller than required
        else if(sum < n) {
            cout << "1\n";
        }

        // Sum is greater than required
        else {
            cout << sum - n << '\n';
        }
    }

    return 0;
}
```

## Test Cases Analysis

| n | Array       | Sum | Answer |
| - | ----------- | --- | ------ |
| 3 | [1,1,1]     | 3   | 0      |
| 4 | [0,0,0,0]   | 0   | 1      |
| 5 | [2,2,2,2,2] | 10  | 5      |
| 1 | [1]         | 1   | 0      |
| 3 | [5,1,1]     | 7   | 4      |

## Edge Cases to Consider

* Single-element array.
* All elements are zero.
* Sum exactly equals `n`.
* Sum much larger than `n`.
* Maximum allowed element values.

## Common Test Cases

* `[1,1,1]`
* `[0,0,0]`
* `[2,2,2]`
* `[5]`
* Mixed-value arrays.

## Common Mistakes to Avoid

* Forgetting that the target sum must be exactly `n`.
* Returning `n - sum` when `sum < n` instead of `1`.
* Misinterpreting the required average condition.

## Interview Relevance

* Tests mathematical reasoning.
* Demonstrates converting an average condition into a sum condition.
* Highlights observation-based problem solving.

## What This Problem Teaches

* Transforming average constraints into sum constraints.
* Identifying simple mathematical patterns.
* Avoiding unnecessary simulation.

## Key Takeaways

* Average `1` implies total sum `n`.
* Compare the current sum directly with the target sum.
* Many array problems simplify significantly after converting averages into sums.

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The implementation is straightforward once the key observation is made that achieving an average of `1` is equivalent to making the total array sum equal to `n`. The rest is simple case analysis based on the relationship between `sum` and `n`.