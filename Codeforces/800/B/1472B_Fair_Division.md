# B_Fair_Division

## Platform

Codeforces

## Problem Link

[B. Fair Division](https://codeforces.com/problemset/problem/1472/B)

## Problem Statement

You are given multiple test cases.
In each test case, there are `n` candies. Each candy has a value of either `1` or `2`.

Your task is to determine whether it is possible to divide all candies into **two groups such that the total value of candies in both groups is equal**.

You must use **all candies**, and each candy must belong to exactly one group.

If such a division is possible, print `YES`; otherwise, print `NO`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`, the number of candies.
  * The second line contains `n` integers, each being either `1` or `2`, representing the value of each candy.

## Output Format

For each test case, print:

* `YES` — if a fair division is possible
* `NO` — otherwise

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 100`
* Each candy value is either `1` or `2`

## Examples

### Example 1

Input

```
3
4
1 1 2 2
3
1 1 1
2
2 2
```

Explanation

* Test case 1:

  * Total sum = 6
  * Can be divided into two groups of sum 3 → possible
* Test case 2:

  * Total sum = 3 (odd) → cannot be divided equally
* Test case 3:

  * Total sum = 4
  * Each group can have one candy of value 2 → possible

Output

```
YES
NO
YES
```

### Example 2

Input

```
1
5
1 2 2 1 2
```

Explanation

* Total sum = 8
* Possible to divide into two groups of sum 4

Output

```
YES
```

## Approach

**Greedy + Parity Analysis**

The solution relies on counting candies of value `1` and `2`, then using parity rules to determine whether an equal division is feasible.

## Intuition

Let:

* `one` = number of candies with value `1`
* `two` = number of candies with value `2`

Key observations:

* The total sum must be **even** to split equally.
* Candies with value `2` always contribute an even amount.
* Candies with value `1` determine whether odd adjustments are possible.

Invalid cases arise when:

* The number of `1`-valued candies is odd.
* There are no `1`-valued candies and the count of `2`-valued candies is odd.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read `n`.
  * Count how many candies have value `1` and how many have value `2`.
  * If:

    * the count of `1`s is odd, **or**
    * there are zero `1`s and the count of `2`s is odd
      → print `NO`
  * Otherwise, print `YES`.

## Visual Walkthrough

### Test Case 1

Candies:

```
1 1 2 2
```

Counts:

```
one = 2
two = 2
```

Total sum:

```
(2 × 1) + (2 × 2) = 6
```

Can split into:

```
Group A: 1 + 2 = 3
Group B: 1 + 2 = 3
```

Result → `YES`

---

### Test Case 2

Candies:

```
1 1 1
```

Counts:

```
one = 3 (odd)
```

Odd number of `1`s prevents equal split → `NO`

---

### Test Case 3

Candies:

```
2 2 2
```

Counts:

```
one = 0
two = 3 (odd)
```

No `1`s to balance an odd number of `2`s → `NO`

## Complexity Analysis

### Time Complexity

**O(n) per test case**

Each candy is processed exactly once to count its value.

### Space Complexity

**O(1)**

Only a few integer counters are used regardless of input size.

## Solution Explanation

The solution reduces the problem to counting and parity checks.
Instead of attempting actual group construction, it analyzes whether such a construction is mathematically possible.
This approach is efficient, simple, and perfectly aligned with the problem constraints.

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

        // Number of candies
        int n;
        cin >> n;

        // Counters for candies of value 1 and 2
        int one = 0, two = 0;

        // Read candy values
        while (n--) {
            int candy;
            cin >> candy;

            if (candy == 1) {
                one++;
            } else {
                two++;
            }
        }

        /*
         Conditions for impossible fair division:
         1) Odd number of '1' candies
         2) No '1' candies and odd number of '2' candies
        */
        if ((one & 1) || (one == 0 && (two & 1))) {
            cout << "NO\n";
        } else {
            cout << "YES\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Candies   | one | two | Result |
| --------- | --------- | --- | --- | ------ |
| 1         | 1 1 2 2   | 2   | 2   | YES    |
| 2         | 1 1 1     | 3   | 0   | NO     |
| 3         | 2 2       | 0   | 2   | YES    |
| 4         | 2 2 2     | 0   | 3   | NO     |
| 5         | 1 2 2 1 2 | 2   | 3   | YES    |

## Edge Cases to Consider

* Only one candy
* All candies have value `1`
* All candies have value `2`
* Large number of candies with mixed values

## Common Test Cases

* Even total sum with mixed candies
* Odd total sum due to `1`s
* No `1`s and odd number of `2`s

## Common Mistakes to Avoid

* Checking only the total sum and ignoring composition
* Assuming any even total sum is always divisible
* Overcomplicating with subset construction

## Interview Relevance

* Tests logical reasoning and parity analysis
* Encourages problem reduction instead of brute force
* Common example of greedy feasibility checking

## What This Problem Teaches

* Importance of parity in partition problems
* How constraints simplify solution design
* Using counting instead of simulation

## Key Takeaways

* Equal partition problems often reduce to parity checks
* Counting-based solutions can outperform constructive approaches
* Understanding constraints leads to elegant logic

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on logical reasoning and basic counting, making it suitable for beginners and a common screening interview question.