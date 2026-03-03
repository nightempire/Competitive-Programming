# A_Array_with_Odd_Sum

## Platform

Codeforces

## Problem Link

[A. Array with Odd Sum](https://codeforces.com/problemset/problem/1296/A)

## Problem Statement

You are given multiple test cases.

For each test case, you are given an array of integers. Determine whether it is possible to select **all elements** such that their total sum is **odd**.

Print `"YES"` if the total sum of the array is odd. Otherwise, print `"NO"`.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * The first line contains an integer `n` — the size of the array.
  * The second line contains `n` integers.

## Output Format

For each test case, print `"YES"` if the array sum is odd, otherwise print `"NO"`.

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n ≤ 100`
* `1 ≤ ai ≤ 100`

## Examples

### Example 1

Input

```
3
3
1 2 3
4
2 4 6 8
5
1 3 5 7 9
```

Explanation

Test Case 1
Sum = 1 + 2 + 3 = 6 → Even → Output: NO

Test Case 2
Sum = 2 + 4 + 6 + 8 = 20 → Even → Output: NO

Test Case 3
Sum = 1 + 3 + 5 + 7 + 9 = 25 → Odd → Output: YES

Output

```
NO
NO
YES
```

---

### Example 2

Input

```
1
4
1 2 4 6
```

Explanation

Sum = 13 → Odd

Output

```
YES
```

---

### Example 3

Input

```
1
3
2 4 6
```

Explanation

All numbers are even → Sum is even → Output: NO

Output

```
NO
```

## Approach

Parity Counting (Mathematical Observation on Odd/Even Properties)

## Intuition

The parity of the total sum depends entirely on how many odd numbers are present.

Key observations:

* The sum of even numbers is always even.
* The sum of odd numbers:

  * Odd count of odd numbers → total sum is odd.
  * Even count of odd numbers → total sum is even.
* To make the total sum odd:

  * There must be at least one odd number.
  * Additionally, either:

    * There exists at least one even number, or
    * The count of odd numbers itself is odd.

Why?

If all numbers are odd:

* Sum parity depends solely on whether the count of odds is odd.

If both even and odd numbers exist:

* The presence of at least one odd guarantees the possibility of odd total sum.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read `n`.
  * Initialize `odd = 0`, `even = 0`.
  * For each element:

    * If element is odd → increment `odd`.
    * Else → increment `even`.
  * If:

    * `odd > 0` AND (`even > 0` OR `odd` is odd)
      → Print `"YES"`
    * Otherwise → Print `"NO"`

## Visual Walkthrough

Consider:

```
1 2 3
```

Odd count = 2
Even count = 1

Since:

```
odd > 0  AND even > 0
```

Answer → YES

---

Consider:

```
1 3 5 7
```

Odd count = 4
Even count = 0

Sum = even (because 4 is even)

Condition:

```
odd > 0  AND (even > 0 OR odd is odd)
```

Here:

```
odd > 0 → true
even > 0 → false
odd is odd → false
```

Final → NO

---

Consider:

```
1 3 5
```

Odd count = 3
Even count = 0

3 is odd → total sum odd → YES

## Complexity Analysis

### Time Complexity

O(n) per test case

Each element is processed once to count parity.

### Space Complexity

O(1)

Only two integer counters are maintained.

## Solution Explanation

The solution does not compute the sum directly.

Instead, it leverages mathematical properties of parity:

* Count how many elements are odd and even.
* Apply logical conditions derived from parity rules.
* Output result accordingly.

This avoids unnecessary addition and keeps the implementation clean and efficient.

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

        // Counters for odd and even numbers
        int odd = 0, even = 0;

        cin >> n;

        // Read elements and count parity
        for (int i = 0; i < n; i++) {

            int num;
            cin >> num;

            // If number is odd, increment odd counter
            if (num & 1)
                odd++;
            else
                even++;
        }

        // Condition to check if total sum can be odd
        // We need at least one odd number
        // And either:
        //  - At least one even number exists
        //  - Or the count of odd numbers is itself odd
        if (odd > 0 && (even > 0 || (odd & 1))) {
            cout << "YES\n";
        } else {
            cout << "NO\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Odd Count | Even Count | Result |
| --------- | --------- | ---------- | ------ |
| 1 2 3     | 2         | 1          | YES    |
| 2 4 6     | 0         | 3          | NO     |
| 1 3 5     | 3         | 0          | YES    |
| 1 3 5 7   | 4         | 0          | NO     |

## Edge Cases to Consider

* All numbers are even
* All numbers are odd
* Single element array
* Only one odd element
* Large number of test cases

## Common Test Cases

* Minimum input size (`n = 1`)
* Mixed parity arrays
* All identical numbers
* Large `t` with small `n`

## Common Mistakes to Avoid

* Checking only `odd % 2 == 1` and ignoring even presence
* Forgetting to reset counters for each test case
* Computing full sum unnecessarily

## Interview Relevance

* Tests understanding of parity mathematics
* Encourages optimization using logical observation
* Common pattern in competitive programming

## What This Problem Teaches

* Importance of mathematical reasoning over brute force
* Efficient counting techniques
* Understanding parity properties

## Key Takeaways

* Sum parity depends only on count of odd numbers
* Avoid unnecessary computation
* Simple logic can replace full summation

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It primarily tests logical reasoning about odd and even properties rather than algorithmic complexity. Ideal for beginners and interview warm-ups.