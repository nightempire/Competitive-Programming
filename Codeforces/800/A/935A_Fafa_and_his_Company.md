# A_Fafa_and_his_Company

## Platform

Codeforces

## Problem Link

[A. Fafa and his Company](https://codeforces.com/problemset/problem/935/A)

## Problem Statement

Fafa owns a company with `n` employees, including himself.

He wants to divide the employees into **two groups**:

* A group of **leaders**
* A group of **regular employees**

The conditions are:

* There must be **at least one leader**.
* There must be **at least one regular employee**.
* Each leader must manage the **same number of employees**.

Your task is to determine **how many possible ways** Fafa can choose the number of leaders such that the conditions above are satisfied.

## Input Format

* A single integer `n` — the total number of employees in the company.

## Output Format

Print a single integer representing the **number of valid ways** to choose leaders.

## Constraints

* `2 ≤ n ≤ 10^5`

## Examples

### Example 1

Input

```
6
```

Explanation

Possible numbers of leaders:

| Leaders | Employees per Leader | Valid |
| ------- | -------------------- | ----- |
| 1       | 5                    | Yes   |
| 2       | 2                    | Yes   |
| 3       | 1                    | Yes   |
| 4       | Not integer          | No    |
| 5       | Not integer          | No    |

Total valid ways = **3**

Output

```
3
```

---

### Example 2

Input

```
3
```

Explanation

Possible leaders:

| Leaders | Employees per Leader | Valid |
| ------- | -------------------- | ----- |
| 1       | 2                    | Yes   |
| 2       | Not integer          | No    |

Total valid ways = **1**

Output

```
1
```

---

### Example 3

Input

```
10
```

Explanation

Possible leaders:

| Leaders | Employees per Leader | Valid |
| ------- | -------------------- | ----- |
| 1       | 9                    | Yes   |
| 2       | 4                    | Yes   |
| 3       | Not integer          | No    |
| 4       | Not integer          | No    |
| 5       | 1                    | Yes   |

Total valid ways = **3**

Output

```
3
```

## Approach

Divisor Counting (Mathematical Observation)

## Intuition

Let:

```
leaders = k
```

Then the remaining employees are:

```
employees = n - k
```

Each leader must manage the **same number of employees**.

Thus:

```
(n - k) must be divisible by k
```

This simplifies to:

```
n = k × (employees_per_leader + 1)
```

Therefore, `k` must be a **divisor of n**.

However:

* `k` must be **less than n**
* Because at least one regular employee must exist.

Thus, the answer equals the **number of divisors of `n` excluding `n` itself**.

This can be computed by checking divisors from `1` to `n/2`.

## Algorithm Steps

* Read integer `n`.
* Initialize `count = 1`.

  * (Leader count = 1 is always valid.)
* Iterate `i` from `2` to `n / 2`:

  * If `n % i == 0`

    * Increment `count`.
* Print `count`.

## Visual Walkthrough

### Test Case 1

Input

```
n = 6
```

Divisors of 6:

```
1, 2, 3, 6
```

Exclude `6` because it would leave no employees.

Valid leaders:

```
1, 2, 3
```

Total ways:

```
3
```

---

### Test Case 2

Input

```
n = 3
```

Divisors:

```
1, 3
```

Exclude `3`.

Valid leaders:

```
1
```

Answer:

```
1
```

---

### Test Case 3

Input

```
n = 10
```

Divisors:

```
1, 2, 5, 10
```

Exclude `10`.

Valid leaders:

```
1, 2, 5
```

Total:

```
3
```

## Complexity Analysis

### Time Complexity

O(n)

The algorithm checks divisibility for values from `2` to `n/2`.

### Space Complexity

O(1)

Only a few integer variables are used.

## Solution Explanation

The key insight is that the number of leaders must evenly divide the total number of employees so that every leader manages the same number of employees.

Thus, we count the divisors of `n` excluding `n` itself.

The program iterates through possible divisors and increments the counter whenever a valid divisor is found.

Finally, the total count is printed.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Total number of employees in the company
    int n;

    // Counter to store number of valid leader choices
    int count = 1;  

    // Read number of employees
    cin >> n;

    // Check divisors from 2 to n/2
    for (int i = 2; i <= n / 2; i++) {

        // If i divides n, it is a valid number of leaders
        if (n % i == 0) {
            count++;
        }
    }

    // Output number of possible leader counts
    cout << count << '\n';

    return 0;
}
```

## Test Cases Analysis

| n  | Divisors     | Valid Leaders | Output |
| -- | ------------ | ------------- | ------ |
| 3  | 1,3          | 1             | 1      |
| 6  | 1,2,3,6      | 1,2,3         | 3      |
| 10 | 1,2,5,10     | 1,2,5         | 3      |
| 12 | 1,2,3,4,6,12 | 1,2,3,4,6     | 5      |

## Edge Cases to Consider

* Minimum value `n = 2`
* Prime numbers
* Large composite numbers
* Numbers with many divisors

## Common Test Cases

* `n = 2`
* `n = 3`
* `n = 10`
* `n = 100`

## Common Mistakes to Avoid

* Including `n` itself as a valid leader count
* Forgetting that at least one employee must remain
* Incorrect divisor loop bounds

## Interview Relevance

* Demonstrates divisor counting
* Reinforces mathematical simplification of problems
* Tests ability to derive constraints from problem statements

## What This Problem Teaches

* Translating real-world constraints into mathematical expressions
* Divisor-based reasoning
* Efficient iteration over possible factors

## Key Takeaways

* Many problems reduce to divisor analysis
* Careful constraint interpretation simplifies logic
* Avoid unnecessary computations when mathematical insight exists

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It primarily requires recognizing the divisor relationship between leaders and employees and implementing a straightforward loop to count valid cases.