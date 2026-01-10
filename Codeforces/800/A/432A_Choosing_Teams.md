# A. Choosing Teams

## Platform

Codeforces

## Problem Link

[https://codeforces.com/problemset/problem/432/A](https://codeforces.com/problemset/problem/432/A)

## Problem Statement

There are `n` students who want to participate in programming contests.
Each student already has participated in some contests.

A student can join a new team **only if the total number of contests they will participate in does not exceed 5**.

You are given:

* `n` – number of students
* `k` – number of upcoming contests
* For each student, the number of contests they have already participated in

Your task is to determine **how many teams of exactly 3 students** can be formed such that **each student in the team is eligible**.

## Input Format

* First line contains two integers `n` and `k`
* Second line contains `n` integers representing contests already participated by each student

## Output Format

Print a single integer representing the **maximum number of teams** that can be formed.

## Constraints

* `1 ≤ n ≤ 2000`
* `0 ≤ k ≤ 5`
* `0 ≤ contests_i ≤ 5`

## Examples

### Example 1

Input

```
6 2
0 4 5 1 0 3
```

Explanation
Eligibility condition:

```
student_contests + k ≤ 5
```

Eligible students:

```
0+2=2 ✔
4+2=6 ✘
5+2=7 ✘
1+2=3 ✔
0+2=2 ✔
3+2=5 ✔
```

Eligible count = 4
Teams possible = `4 / 3 = 1`

Output

```
1
```

### Example 2

Input

```
3 3
2 2 2
```

Explanation
Each student:

```
2+3 = 5 ✔
```

Eligible count = 3
Teams possible = `3 / 3 = 1`

Output

```
1
```

### Example 3

Input

```
5 5
0 0 0 0 0
```

Explanation
All students:

```
0+5 = 5 ✔
```

Eligible count = 5
Teams possible = `5 / 3 = 1`

Output

```
1
```

## Approach (Algorithm Type)

Greedy counting with eligibility filtering.

## Intuition

Each student is evaluated independently.
If a student is eligible, they are counted.
Once all eligible students are counted, every **group of 3 students forms one team**.

There is no dependency between students, so sorting or pairing is unnecessary.

## Algorithm Steps

* Read `n` and `k`
* Initialize a counter for eligible students
* For each student:

  * Read the number of contests already participated
  * If `(contests + k) ≤ 5`, increment the counter
* Divide the eligible count by 3 to get the number of teams
* Print the result

## Visual Walkthrough

Test Case 1:

```
n = 6, k = 2
[0, 4, 5, 1, 0, 3]
```

Eligibility check:

```
✔ ✘ ✘ ✔ ✔ ✔
```

Eligible students:

```
4
```

Teams:

```
4 / 3 = 1
```

---

Test Case 2:

```
n = 3, k = 3
[2, 2, 2]
```

Eligibility:

```
✔ ✔ ✔
```

Teams:

```
3 / 3 = 1
```

---

Test Case 3:

```
n = 4, k = 1
[5, 5, 5, 5]
```

Eligibility:

```
✘ ✘ ✘ ✘
```

Teams:

```
0
```

## Complexity Analysis

### Time Complexity

O(n)
Each student is checked exactly once.

### Space Complexity

O(1)
Only constant extra variables are used.

## Solution Explanation

The solution filters students based on eligibility using the condition
`contests_participated + k ≤ 5`.

Eligible students are counted, and since each team requires exactly 3 members, integer division by 3 gives the maximum number of teams.

This approach is optimal, simple, and fully aligned with the problem constraints.

## Full Solution (Heavily Commented C++ Code)

```cpp
#include <iostream>
using namespace std;

int main() {

    // n -> number of students
    // k -> number of upcoming contests
    int n, k;

    // Counter to store how many students are eligible
    int count = 0;

    // Read input values
    cin >> n >> k;

    // Loop through all students
    for (int i = 0; i < n; i++) {

        // Number of contests already participated by the student
        int num;
        cin >> num;

        // Eligibility check:
        // A student can participate only if total contests <= 5
        if (num + k <= 5) {
            count++;
        }
    }

    // Each team requires exactly 3 eligible students
    // Integer division gives the maximum number of teams
    cout << count / 3;

    return 0;
}
```

## Test Cases Analysis

| Students (n) | k | Eligible Students | Teams Formed |
| ------------ | - | ----------------- | ------------ |
| 3            | 3 | 3                 | 1            |
| 6            | 2 | 4                 | 1            |
| 5            | 5 | 5                 | 1            |
| 4            | 1 | 2                 | 0            |

## Edge Cases to Consider

* No student is eligible
* Eligible students less than 3
* All students are eligible
* Maximum input size

## Common Test Cases

* Mixed eligibility
* Exactly 3 eligible students
* Large `n` with zero eligible students

## Common Mistakes to Avoid

* Using `< 5` instead of `≤ 5`
* Forgetting integer division by 3
* Counting teams inside the loop

## Interview Relevance

* Tests conditional filtering logic
* Demonstrates greedy counting
* Evaluates basic input handling and constraints awareness

## What This Problem Teaches

* Translating constraints into conditions
* Efficient counting strategies
* Avoiding unnecessary data structures

## Key Takeaways

* Simple conditions often eliminate complex logic
* Count first, divide later
* Always align checks exactly with constraints

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic logic, loops, and condition checks, making it ideal for beginners and technical interview warm-ups.