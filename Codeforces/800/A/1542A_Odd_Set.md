# 1542A_Odd_Set

## Platform

Codeforces

## Problem Link

[A. Odd Set](https://codeforces.com/problemset/problem/1542/A)

## Problem Statement

You are given `2n` integers.

Your task is to determine whether it is possible to choose **exactly `n` odd numbers** from the given `2n` integers.

If the number of odd integers in the array is **exactly `n`**, print `"YES"`.
Otherwise, print `"NO"`.

## Input Format

* The first line contains an integer `t`, the number of test cases
* For each test case:

  * An integer `n`
  * `2n` integers

## Output Format

* For each test case, print `"YES"` if exactly `n` numbers are odd
* Otherwise, print `"NO"`

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 50`
* Integers can be positive, negative, or zero

## Examples

### Example 1

Input

```
1
2
1 2 3 4
```

Explanation

Total numbers = `4`
Odd numbers = `{1, 3}` → count = `2`
Since `2 = n`, the condition is satisfied.

Output

```
YES
```

---

### Example 2

Input

```
1
3
2 4 6 8 10 12
```

Explanation

All numbers are even.
Odd count = `0`, which is not equal to `n = 3`.

Output

```
NO
```

---

### Example 3

Input

```
1
1
7 9
```

Explanation

Odd numbers = `{7, 9}` → count = `2`
Required odd count = `1`.

Output

```
NO
```

## Approach

**Counting Odd Numbers**

## Intuition

The problem reduces to a simple observation:

* You are given exactly `2n` numbers
* You need **exactly `n` odd numbers**

So the only thing that matters is:

* Count how many numbers are odd
* Compare this count with `n`

No rearrangement or selection strategy is required.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read `n`
  * Set total numbers to `2n`
  * Initialize an odd counter
  * Read all `2n` numbers and count how many are odd
  * If odd count equals `n`, print `"YES"`
  * Otherwise, print `"NO"`

## Visual Walkthrough

### Case 1: `n = 2`, numbers = `1 2 3 4`

```
Odd numbers: 1, 3
Odd count = 2
Required = 2
→ YES
```

---

### Case 2: `n = 2`, numbers = `2 4 6 7`

```
Odd numbers: 7
Odd count = 1
Required = 2
→ NO
```

---

### Case 3: `n = 1`, numbers = `5 6`

```
Odd numbers: 5
Odd count = 1
Required = 1
→ YES
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each of the `2n` numbers is processed once.

### Space Complexity

**O(1)**

Only a constant counter variable is used.

## Solution Explanation

The solution directly counts how many odd numbers appear in the input.

Because the condition requires **exact equality** between the number of odd values and `n`, a simple comparison determines the result.

This direct counting approach is optimal and avoids unnecessary complexity.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int n;
        cin >> n;

        // Total numbers = 2n
        int total = 2 * n;

        // Counter for odd numbers
        int odd = 0;

        // Read all numbers and count odds
        for (int i = 0; i < total; i++) {
            int num;
            cin >> num;
            if (num & 1) odd++;
        }

        // Check if exactly n numbers are odd
        cout << (odd == n ? "YES\n" : "NO\n");
    }

    return 0;
}
```

## Test Cases Analysis

| n | Numbers         | Odd Count | Output |
| - | --------------- | --------- | ------ |
| 2 | `1 2 3 4`       | 2         | YES    |
| 3 | `2 4 6 8 10 12` | 0         | NO     |
| 1 | `7 9`           | 2         | NO     |
| 1 | `5 6`           | 1         | YES    |

## Edge Cases to Consider

* All numbers odd
* All numbers even
* Minimum value of `n`
* Multiple test cases

## Common Test Cases

* Mixed odd and even values
* Large number of test cases
* Random ordering of numbers

## Common Mistakes to Avoid

* Forgetting that total numbers are `2n`
* Using `>= n` instead of `== n`
* Miscounting odd numbers

## Interview Relevance

* Tests basic number theory (parity)
* Evaluates input handling and counting logic
* Common beginner-level screening problem

## What This Problem Teaches

* Importance of precise condition checking
* Efficient counting strategies
* Translating problem constraints directly into logic

## Key Takeaways

* Only the count of odd numbers matters
* Exact equality conditions must be handled carefully
* Simple solutions are often the best

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It requires basic understanding of parity and counting, making it ideal for beginners and quick competitive programming practice.