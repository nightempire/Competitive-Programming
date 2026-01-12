# A_Die_Roll

## Platform

Codeforces

## Problem Link

[A. Die Roll](https://codeforces.com/problemset/problem/9/A)

## Problem Statement

Yakko and Wakko roll a standard six-faced die.

* Yakko rolls a number `y`
* Wakko rolls a number `w`

The winner is decided by rolling **one more die**.
Yakko wins if the number rolled is **greater than or equal to** the maximum of `y` and `w`.

Your task is to compute the **probability** that Yakko wins and output it as a **reduced fraction**.

## Input Format

* A single line containing two integers `y` and `w`

## Output Format

Print the probability that Yakko wins in the form of a reduced fraction `a/b`.

## Constraints

* `1 ≤ y, w ≤ 6`

## Examples

### Example 1

Input

```
4 2
```

Explanation

* Maximum of `y` and `w` = `4`
* Favorable outcomes = `{4, 5, 6}` → 3 outcomes
* Total outcomes = 6

Probability

```
3 / 6 = 1 / 2
```

Output

```
1/2
```

### Example 2

Input

```
6 6
```

Explanation

* Maximum = `6`
* Favorable outcomes = `{6}` → 1 outcome

Probability

```
1 / 6
```

Output

```
1/6
```

### Example 3

Input

```
1 1
```

Explanation

* Maximum = `1`
* Favorable outcomes = `{1,2,3,4,5,6}` → 6 outcomes

Probability

```
6 / 6 = 1 / 1
```

Output

```
1/1
```

## Approach (Algorithm Name / Type)

**Direct Probability Mapping with Conditional Logic**

## Intuition

A die has exactly **6 outcomes**.

Once the maximum of `y` and `w` is known, all values **greater than or equal to it** are winning outcomes for Yakko.

Instead of computing and simplifying fractions dynamically, we can directly map the number of favorable outcomes to their **already reduced fractional forms**, since the possible cases are very limited.

## Algorithm Steps

* Read integers `y` and `w`
* Compute `m = max(y, w)`
* Compute favorable outcomes as `6 - m`
* Use conditional checks to print the corresponding reduced fraction
* Handle all possible favorable counts explicitly

## Visual Walkthrough

### Test Case 1

Input

```
y = 4, w = 2
```

Maximum

```
max(4, 2) = 4
```

Winning outcomes

```
{4, 5, 6}
```

Favorable outcomes = 3
Probability

```
3/6 → 1/2
```

---

### Test Case 2

Input

```
y = 6, w = 6
```

Maximum

```
6
```

Winning outcomes

```
{6}
```

Probability

```
1/6
```

---

### Test Case 3

Input

```
y = 1, w = 1
```

Winning outcomes

```
{1,2,3,4,5,6}
```

Probability

```
6/6 → 1/1
```

## Complexity Analysis

### Time Complexity

**O(1)**
Only constant-time operations are performed.

### Space Complexity

**O(1)**
No additional memory is used.

## Solution Explanation

The solution calculates the number of favorable outcomes based on the maximum of the two initial rolls.
Since there are only six possible outcomes, each favorable count corresponds to a known reduced fraction, which is printed directly.

This avoids unnecessary fraction simplification logic and keeps the implementation clean and efficient.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // y and w represent the values rolled by Yakko and Wakko
    int y, w;
    cin >> y >> w;

    // Calculate number of favorable outcomes
    // Favorable outcomes are values >= max(y, w)
    int fav = 6 - max(y, w);

    // Print the reduced fraction based on favorable outcomes
    if (fav == 0)
        cout << "1/6";      // Only one outcome (rolling 6)
    else if (fav == 1)
        cout << "1/3";      // 2 favorable outcomes -> 2/6 = 1/3
    else if (fav == 2)
        cout << "1/2";      // 3/6 = 1/2
    else if (fav == 3)
        cout << "2/3";      // 4/6 = 2/3
    else if (fav == 4)
        cout << "5/6";      // 5/6
    else
        cout << "1/1";      // 6/6 = 1/1

    return 0;
}
```

## Test Cases Analysis

| y | w | Max | Favorable Outcomes | Probability |
| - | - | --- | ------------------ | ----------- |
| 1 | 1 | 1   | 6                  | 1/1         |
| 2 | 3 | 3   | 4                  | 2/3         |
| 4 | 2 | 4   | 3                  | 1/2         |
| 6 | 6 | 6   | 1                  | 1/6         |

## Edge Cases to Consider

* Both players roll the same value
* One player rolls `6`
* Both players roll `1`

## Common Test Cases

* `(y, w) = (1, 1)`
* `(y, w) = (6, 6)`
* `(y, w) = (3, 5)`

## Common Mistakes to Avoid

* Forgetting to reduce the fraction
* Using incorrect favorable outcome calculation
* Misinterpreting the winning condition (`>= max(y, w)`)

## Interview Relevance

* Tests understanding of probability fundamentals
* Evaluates conditional logic
* Demonstrates optimization through precomputed results

## What This Problem Teaches

* Mapping mathematical outcomes to code logic
* Handling probability problems efficiently
* Recognizing when direct enumeration is sufficient

## Key Takeaways

* Small constraint problems benefit from direct mapping
* Reduced fractions simplify output correctness
* Clear logic often outperforms generic solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It requires basic probability reasoning and simple conditional logic, making it suitable for beginners and interview warm-ups.