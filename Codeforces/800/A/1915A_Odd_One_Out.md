# A_Odd_One_Out

## Platform

Codeforces

## Problem Link

[A. Odd One Out](https://codeforces.com/problemset/problem/1915/A)

## Problem Statement

You are given multiple test cases.
In each test case, three integers are provided.

Among these three numbers, **exactly two numbers are equal**, and **one number is different**.

Your task is to determine and print the number that is **different** from the other two.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains three integers `a`, `b`, and `c`.

## Output Format

For each test case, print a single integer — the number that appears **only once**.

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `0 ≤ a, b, c ≤ 10^9`
* In each test case, **exactly two numbers are equal**

## Examples

### Example 1

Input

```
3
1 1 2
4 5 4
7 3 3
```

Explanation

* Test case 1: `1, 1, 2` → odd one out is `2`
* Test case 2: `4, 5, 4` → odd one out is `5`
* Test case 3: `7, 3, 3` → odd one out is `7`

Output

```
2
5
7
```

### Example 2

Input

```
1
100 200 100
```

Explanation

* Two numbers are `100`
* The different number is `200`

Output

```
200
```

## Approach (Algorithm Name / Type)

**Bitwise XOR-Based Identification Algorithm**

This approach leverages the properties of the XOR (`^`) operator to isolate the unique value.

## Intuition

The XOR operator has two important properties:

* `x ^ x = 0`
* `x ^ 0 = x`

Since exactly two numbers are equal in each test case, XOR-ing all three numbers causes the duplicate values to cancel out, leaving only the unique number.

This makes XOR an ideal and elegant solution for this problem.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read integers `a`, `b`, and `c`.
  * Compute `a ^ b ^ c`.
  * Print the result, which represents the odd one out.

## Visual Walkthrough

### Test Case 1

Input:

```
a = 1, b = 1, c = 2
```

XOR computation:

```
1 ^ 1 = 0
0 ^ 2 = 2
```

Result:

```
2
```

---

### Test Case 2

Input:

```
a = 4, b = 5, c = 4
```

XOR computation:

```
4 ^ 4 = 0
0 ^ 5 = 5
```

Result:

```
5
```

---

### Test Case 3

Input:

```
a = 7, b = 3, c = 3
```

XOR computation:

```
3 ^ 3 = 0
0 ^ 7 = 7
```

Result:

```
7
```

## Complexity Analysis

### Time Complexity

**O(t)**

Each test case requires a constant number of operations.
The total time complexity grows linearly with the number of test cases.

### Space Complexity

**O(1)**

Only constant extra space is used.
No additional data structures are required.

## Solution Explanation

The solution applies the XOR operation to all three numbers in a test case.

Because the problem guarantees that exactly two values are the same, the XOR operation eliminates the duplicate pair and leaves behind the unique number. This results in a concise, efficient, and highly reliable solution.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Read three integers
        int a, b, c;
        cin >> a >> b >> c;

        // XOR operation:
        // - Identical numbers cancel each other out
        // - The remaining value is the unique one
        int oddOneOut = a ^ b ^ c;

        // Output the result
        cout << oddOneOut << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input         | XOR Result | Explanation               | Output |
| ------------- | ---------- | ------------------------- | ------ |
| `1 1 2`       | `2`        | Duplicate 1 cancels out   | 2      |
| `4 5 4`       | `5`        | Duplicate 4 cancels out   | 5      |
| `7 3 3`       | `7`        | Duplicate 3 cancels out   | 7      |
| `100 200 100` | `200`      | Duplicate 100 cancels out | 200    |

## Edge Cases to Consider

* The unique number appears in the first position
* The unique number appears in the middle
* The unique number appears in the last position

## Common Test Cases

* Two small equal numbers and one large number
* Two large equal numbers and one small number
* Mixed ordering of inputs

## Common Mistakes to Avoid

* Using conditional comparisons instead of XOR
* Forgetting that exactly two numbers are guaranteed to be equal
* Misunderstanding XOR behavior with duplicate values

## Interview Relevance

* Tests understanding of bitwise operators
* Common trick question in technical interviews
* Demonstrates ability to write concise and optimal code

## What This Problem Teaches

* Practical application of bitwise XOR
* Leveraging mathematical properties for cleaner solutions
* Avoiding unnecessary branching logic

## Key Takeaways

* XOR is a powerful tool for identifying unique elements
* Mathematical properties can significantly simplify logic
* Elegant solutions are often the most efficient

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It is designed to introduce bitwise operations in a practical context and is frequently used as a warm-up or screening problem in competitive programming and interviews.