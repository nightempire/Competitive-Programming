# A. Legs

## Platform

Codeforces

## Problem Link

[A. Legs](https://codeforces.com/problemset/problem/1660/A)

## Problem Statement

You are given multiple test cases.
For each test case, you are given an integer `n`, representing the total number of legs.

There are two types of animals:

* One animal has **2 legs**
* Another animal has **4 legs**

Your task is to determine the **minimum number of animals** required such that the total number of legs is exactly `n`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains a single integer `n`.

## Output Format

For each test case, print a single integer — the **minimum number of animals** needed.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 10^9`
* `n` is always even

## Examples

### Example 1

Input

```
3
2
4
6
```

Explanation

* `n = 2` → one 2-legged animal
* `n = 4` → one 4-legged animal
* `n = 6` → one 4-legged + one 2-legged animal

Output

```
1
1
2
```

### Example 2

Input

```
2
8
10
```

Explanation

* `n = 8` → two 4-legged animals
* `n = 10` → two 4-legged + one 2-legged animal

Output

```
2
3
```

## Approach

Greedy division using maximum legs per animal.

## Intuition

To minimize the number of animals:

* Prefer animals with **4 legs**, as they contribute more legs per animal
* Use as many 4-legged animals as possible
* If there is a remaining `2` legs, add one 2-legged animal

This greedy choice guarantees the minimum count.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Compute the number of 4-legged animals as `n / 4`
  * If `n % 4 == 2`, add one 2-legged animal
  * Output the total number of animals

## Visual Walkthrough

### Test Case 1

Input:

```
n = 6
```

Calculation:

```
6 / 4 = 1 (one 4-legged animal)
6 % 4 = 2 (one 2-legged animal)
```

Total animals:

```
1 + 1 = 2
```

---

### Test Case 2

Input:

```
n = 10
```

Calculation:

```
10 / 4 = 2 (two 4-legged animals)
10 % 4 = 2 (one 2-legged animal)
```

Total animals:

```
3
```

---

### Test Case 3

Input:

```
n = 4
```

Calculation:

```
4 / 4 = 1
4 % 4 = 0
```

Total animals:

```
1
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case is processed using constant-time arithmetic operations.

### Space Complexity

O(1)

Only a few integer variables are used.

## Solution Explanation

The solution greedily uses animals with 4 legs to cover as many legs as possible.
Any remaining legs (which can only be `2`) are handled by adding one 2-legged animal.

This guarantees the minimum number of animals for every valid input.

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

        // Total number of legs
        int n;
        cin >> n;

        // Maximum number of 4-legged animals
        int fourLegged = n / 4;

        // Check if a 2-legged animal is needed
        int twoLegged = (n % 4) / 2;

        // Output the minimum number of animals
        cout << fourLegged + twoLegged << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n  | Output | Explanation         |
| -- | ------ | ------------------- |
| 2  | 1      | One 2-legged animal |
| 4  | 1      | One 4-legged animal |
| 6  | 2      | 4 + 2               |
| 8  | 2      | Two 4-legged        |
| 10 | 3      | 4 + 4 + 2           |

## Edge Cases to Consider

* `n = 2`
* `n = 4`
* Very large values of `n`

## Common Test Cases

* Multiples of 4
* Values leaving remainder 2
* Large even numbers

## Common Mistakes to Avoid

* Forgetting that `n` is always even
* Using too many 2-legged animals
* Overcomplicating the logic

## Interview Relevance

* Tests greedy problem-solving
* Evaluates basic arithmetic reasoning
* Common logic-based counting problem

## What This Problem Teaches

* Greedy strategies for minimization
* Efficient use of division and modulo
* Translating word problems into arithmetic logic

## Key Takeaways

* Always use the largest units first to minimize count
* Modulo operations simplify remainder handling
* Simple arithmetic can solve optimization problems

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on greedy arithmetic reasoning and clean implementation rather than complex algorithms.