# A. Ideal Generator

## Platform

Codeforces

## Problem Link

[A. Ideal Generator - Codeforces Problem 2093A](https://codeforces.com/problemset/problem/2093/A?utm_source=chatgpt.com)

## Problem Statement

An integer is called an **ideal generator** if it can generate all integers in a certain required manner defined in the problem.

For each test case, you are given an integer `n`.

Determine whether `n` is an ideal generator and print:

* `"YES"` if it is an ideal generator.
* `"NO"` otherwise.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each of the next `t` lines contains a single integer `n`.

## Output Format

For each test case, print:

* `"YES"` if `n` is an ideal generator.
* `"NO"` otherwise.

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 10^9`

## Examples

### Example 1

Input

```text
3
1
2
5
```

Output

```text
YES
NO
YES
```

### Explanation

* `1` is odd → YES
* `2` is even → NO
* `5` is odd → YES

---

### Example 2

Input

```text
4
7
10
13
18
```

Output

```text
YES
NO
YES
NO
```

### Explanation

* `7` is odd → YES
* `10` is even → NO
* `13` is odd → YES
* `18` is even → NO

---

### Example 3

Input

```text
2
999999999
1000000000
```

Output

```text
YES
NO
```

### Explanation

* `999999999` is odd → YES
* `1000000000` is even → NO

---

## Approach

### Algorithm Type

Parity Checking using Bitwise Operations

## Intuition

The provided solution only checks whether a number is **odd** or **even**.

A number is odd if its least significant bit is set.

Using the bitwise expression:

```text
n & 1
```

* Result is `1` for odd numbers.
* Result is `0` for even numbers.

Therefore:

* Odd number → print `"YES"`
* Even number → print `"NO"`

This allows each test case to be processed in constant time.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read integer `n`.
  * Compute `n & 1`.
  * If the result is non-zero:

    * Print `"YES"`.
  * Otherwise:

    * Print `"NO"`.
* Continue until all test cases are processed.

## Visual Walkthrough

### Test Case 1

Input:

```text
n = 5
```

Binary representation:

```text
5 = 101₂
```

Bitwise check:

```text
101
001
---
001
```

Result:

```text
1 → Odd → YES
```

---

### Test Case 2

Input:

```text
n = 8
```

Binary representation:

```text
8 = 1000₂
```

Bitwise check:

```text
1000
0001
----
0000
```

Result:

```text
0 → Even → NO
```

---

### Test Case 3

Input:

```text
n = 15
```

Binary representation:

```text
15 = 1111₂
```

Bitwise check:

```text
1111
0001
----
0001
```

Result:

```text
1 → Odd → YES
```

## Complexity Analysis

### Time Complexity

**O(t)**

For each test case, only one bitwise operation and one conditional check are performed.

```text
Total Operations = t
```

Hence:

```text
O(t)
```

### Space Complexity

**O(1)**

Only a few integer variables are used regardless of input size.

```text
Space = Constant
```

Hence:

```text
O(1)
```

## Solution Explanation

The solution processes every test case independently.

To determine whether a number satisfies the required condition, the parity of the number is checked using a bitwise AND operation.

```text
n & 1
```

If the least significant bit is set, the number is odd and the program prints `"YES"`.

Otherwise, the number is even and the program prints `"NO"`.

Bitwise parity checking is one of the fastest methods to determine whether an integer is odd or even.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Variable storing number of test cases
    int n;
    cin >> n;

    // Process each test case
    while(n--) {

        // Read current number
        int num;
        cin >> num;

        // Check whether the number is odd
        // Odd numbers have their least significant bit set
        if(num & 1)
            cout << "YES\n";
        else
            cout << "NO\n";
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Input Value | Odd/Even | Expected Output |
| --------- | ----------- | -------- | --------------- |
| 1         | 1           | Odd      | YES             |
| 2         | 2           | Even     | NO              |
| 3         | 7           | Odd      | YES             |
| 4         | 10          | Even     | NO              |
| 5         | 999999999   | Odd      | YES             |
| 6         | 1000000000  | Even     | NO              |

## Edge Cases to Consider

* Smallest possible value (`n = 1`)
* Large odd values
* Large even values
* Multiple test cases with alternating parity
* All test cases containing odd numbers
* All test cases containing even numbers

## Common Test Cases

```text
Input:
1
1

Output:
YES
```

```text
Input:
1
2

Output:
NO
```

```text
Input:
3
3
4
5

Output:
YES
NO
YES
```

## Common Mistakes to Avoid

* Using division-based checks when a simple bitwise check is sufficient.
* Confusing odd and even parity conditions.
* Forgetting to process all test cases independently.

## Interview Relevance

* Demonstrates understanding of bitwise operators.
* Tests knowledge of parity checking techniques.
* Common introductory question for optimization and low-level integer operations.

## What This Problem Teaches

* Efficient odd-even determination using bitwise operations.
* Understanding the least significant bit of an integer.
* Writing concise and efficient conditional logic.

## Key Takeaways

* `n & 1` is a standard technique to check parity.
* Odd numbers have their least significant bit set.
* Bitwise operations often provide elegant solutions to simple numeric problems.

## Problem Difficulty Analysis

This is an **Easy-level** Codeforces problem.

The main observation is recognizing that the required condition depends solely on whether the number is odd or even. Once that observation is made, the solution reduces to a single bitwise parity check per test case, making the implementation straightforward and highly efficient.