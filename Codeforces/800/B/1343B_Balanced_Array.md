# B_Balanced_Array

## Platform

Codeforces

## Problem Link

[B. Balanced Array](https://codeforces.com/problemset/problem/1343/B)

## Problem Statement

You are given an integer `n`.
Your task is to construct an array of `n` **distinct positive integers** such that:

* The **sum of the first `n / 2` elements** is equal to the
* **sum of the last `n / 2` elements**

If it is **not possible**, print `NO`.
Otherwise, print `YES` followed by the required array.

Each test case is independent.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * A single integer `n` is given.

## Output Format

* For each test case:

  * Print `NO` if a balanced array cannot be constructed.
  * Otherwise:

    * Print `YES`
    * Print `n` space-separated integers representing the balanced array.

## Constraints

* `1 ≤ t ≤ 1000`
* `2 ≤ n ≤ 50`
* `n` is even

## Examples

### Example 1

Input

```
1
4
```

Explanation

* First half (even numbers): `2 4` → sum = `6`
* Second half (odd numbers): `1 5` → sum = `6`
* Both halves are balanced.

Output

```
YES
2 4 1 5
```

---

### Example 2

Input

```
1
6
```

Explanation

* First half: `2 4 6` → sum = `12`
* Second half constructed as `1 3 8` → sum = `12`
* Balanced array exists.

Output

```
YES
2 4 6 1 3 8
```

---

### Example 3

Input

```
1
2
```

Explanation

* Cannot divide into two halves with equal sums.
* Condition fails.

Output

```
NO
```

## Approach

**Greedy Construction with Arithmetic Balancing**

## Intuition

To guarantee equal sums:

* Use **even numbers** for the first half.
* Use **odd numbers** for the second half.
* Carefully adjust the **last element** of the second half so total sums match.

Observation:
A balanced array is possible **only when `n` is divisible by 4**.

## Algorithm Steps

* Read number of test cases `t`.
* For each test case:

  * Read `n`.
  * If `n % 4 != 0`, print `NO` and continue.
  * Otherwise:

    * Print `YES`.
    * Add the first `n/2` even numbers.
    * Compute their sum.
    * Add the first `(n/2 - 1)` odd numbers.
    * Compute the remaining value required to balance the sums.
    * Print the final balancing number.

## Visual Walkthrough

### Test Case 1: `n = 4`

First half (even numbers):

```
2 4  → sum = 6
```

Second half (odd numbers):

```
1
Remaining value = 6 - 1 = 5
```

Final array:

```
2 4 1 5
```

---

### Test Case 2: `n = 6`

First half:

```
2 4 6 → sum = 12
```

Second half (partial):

```
1 3 → sum = 4
```

Remaining value:

```
12 - 4 = 8
```

Final array:

```
2 4 6 1 3 8
```

## Complexity Analysis

### Time Complexity

**O(n) per test case**

* Each number is generated and printed once.

### Space Complexity

**O(1)**

* Only a few integer variables are used.
* No auxiliary data structures.

## Solution Explanation

The solution ensures balance by:

* Assigning even numbers to one half to create a predictable sum.
* Assigning odd numbers to the other half.
* Adjusting the final element so that both halves have equal total values.

The divisibility condition (`n % 4 == 0`) guarantees feasibility.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Size of the array
        int n;
        cin >> n;

        // If n is not divisible by 4, balanced array is impossible
        if (n % 4 != 0) {
            cout << "NO\n";
            continue;
        }

        // Balanced array is possible
        cout << "YES\n";

        int sum = 0;

        // First half: print n/2 even numbers
        for (int i = 2; i <= n; i += 2) {
            cout << i << " ";
            sum += i; // Accumulate sum of even numbers
        }

        // Second half: print first (n/2 - 1) odd numbers
        for (int i = 1; i < n / 2; i++) {
            int odd = i * 2 - 1;
            cout << odd << " ";
            sum -= odd; // Subtract odd numbers from total sum
        }

        // Last number balances the sum
        cout << sum << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n | Feasibility | Output Type | Reason             |
| - | ----------- | ----------- | ------------------ |
| 2 | No          | NO          | Cannot balance     |
| 4 | Yes         | YES         | Smallest valid     |
| 6 | No          | NO          | Not divisible by 4 |
| 8 | Yes         | YES         | Balanced possible  |

## Edge Cases to Consider

* Minimum even value (`n = 2`)
* Large valid values (`n = 50`)
* Multiple test cases

## Common Test Cases

* `n` divisible by 4
* `n` not divisible by 4
* Single test case vs multiple test cases

## Common Mistakes to Avoid

* Ignoring the `n % 4` feasibility condition
* Printing incorrect last balancing value
* Using duplicate numbers

## Interview Relevance

* Demonstrates greedy construction
* Tests arithmetic reasoning
* Evaluates constraint-based feasibility analysis

## What This Problem Teaches

* Importance of mathematical observation
* Controlled construction of arrays
* Efficient problem-solving without extra memory

## Key Takeaways

* Not all constraints guarantee a solution
* Greedy methods can simplify array construction
* Mathematical validation is crucial before implementation

## Problem Difficulty Analysis

This is a **Medium-level** problem.
It requires logical insight and mathematical validation rather than brute-force computation.