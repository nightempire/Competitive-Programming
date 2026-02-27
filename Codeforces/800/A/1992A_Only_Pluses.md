# A_Only_Pluses

## Platform

Codeforces

## Problem Link

[A. Only Pluses](https://codeforces.com/problemset/problem/1992/A)

---

## Problem Statement

You are given three integers `a`, `b`, and `c`.

You are allowed to perform exactly **5 operations**.
In each operation, you can choose **one** of the three numbers and increase it by `1`.

After performing all 5 operations, your goal is to **maximize the product**:

```
a × b × c
```

Print the maximum possible product after 5 increments.

---

## Input Format

* The first line contains an integer `t` — number of test cases.
* For each test case:

  * Three integers `a`, `b`, `c`.

---

## Output Format

For each test case, print the maximum possible value of:

```
a × b × c
```

after exactly 5 increment operations.

---

## Constraints

* `1 ≤ t ≤ 1000`
* `0 ≤ a, b, c ≤ 100`

---

## Examples

### Example 1

Input

```
2
1 2 3
0 0 0
```

Explanation

Test Case 1:

Start: `(1, 2, 3)`

We increment the smallest number each time:

Step-by-step balancing:

```
(1,2,3)
(2,2,3)
(2,3,3)
(3,3,3)
(4,3,3)
(4,4,3)
```

Final product:

```
4 × 4 × 3 = 48
```

Test Case 2:

Start: `(0,0,0)`

After distributing increments evenly:

```
(2,2,1)
```

Product:

```
2 × 2 × 1 = 4
```

Output

```
48
4
```

---

## Approach (Algorithm Type)

**Greedy Strategy (Balancing Technique for Product Maximization)**

---

## Intuition

To maximize the product of three numbers under limited increments:

* The product is maximized when the numbers are as balanced as possible.
* Increasing the smallest number gives the highest marginal product gain.

Mathematically:

For fixed total sum, the product is maximized when values are as equal as possible.

Thus, at each operation:

* Increment the smallest among `a`, `b`, and `c`.

Repeat 5 times.

---

## Why Greedy Works

If one number is significantly smaller:

* Increasing it increases the product more than increasing a larger number.
* Because multiplication amplifies imbalance.

Example:

Compare:

```
1 × 5 × 5 = 25
2 × 5 × 5 = 50   (doubling effect)
```

Versus increasing a large number:

```
1 × 6 × 5 = 30
```

Clearly, boosting the smallest element gives better product growth.

---

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read integers `a`, `b`, `c`.
  * Repeat 5 times:

    * Find the smallest among `a`, `b`, `c`.
    * Increment it by 1.
  * Print `a × b × c`.

---

## Visual Walkthrough

### Test Case 1

Input:

```
1 2 3
```

Operations:

| Step  | a | b | c |
| ----- | - | - | - |
| Start | 1 | 2 | 3 |
| 1     | 2 | 2 | 3 |
| 2     | 2 | 3 | 3 |
| 3     | 3 | 3 | 3 |
| 4     | 4 | 3 | 3 |
| 5     | 4 | 4 | 3 |

Final Product:

```
4 × 4 × 3 = 48
```

---

### Test Case 2

Input:

```
0 0 0
```

Operations:

```
(0,0,0)
(1,0,0)
(1,1,0)
(1,1,1)
(2,1,1)
(2,2,1)
```

Final Product:

```
2 × 2 × 1 = 4
```

---

### Test Case 3

Input:

```
5 5 5
```

Operations:

```
(6,5,5)
(6,6,5)
(6,6,6)
(7,6,6)
(7,7,6)
```

Product:

```
7 × 7 × 6 = 294
```

---

## Complexity Analysis

### Time Complexity

Each test case:

* Exactly 5 iterations (constant work).

Overall:

```
O(t)
```

---

### Space Complexity

```
O(1)
```

Only three integer variables used.

---

## Solution Explanation

The solution applies a greedy balancing strategy:

* During each of the 5 increments:

  * Compare the three numbers.
  * Increment the smallest one.
* After 5 operations:

  * Compute the product.

This guarantees maximum possible product under constraints.

---

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        int a, b, c;
        cin >> a >> b >> c;

        // Perform exactly 5 increment operations
        for(int i = 0; i < 5; i++) {

            // Increment the smallest value
            if(a <= b && a <= c) {
                a++;
            }
            else if(b <= a && b <= c) {
                b++;
            }
            else {
                c++;
            }
        }

        // Output maximum product
        cout << a * b * c << "\n";
    }

    return 0;
}
```

---

## Test Cases Analysis

| a  | b | c | Final Values | Product |
| -- | - | - | ------------ | ------- |
| 1  | 2 | 3 | 4 4 3        | 48      |
| 0  | 0 | 0 | 2 2 1        | 4       |
| 5  | 5 | 5 | 7 7 6        | 294     |
| 10 | 1 | 1 | 10 4 4       | 160     |

---

## Edge Cases to Consider

* All zeros
* All equal values
* One value much larger than others
* Large initial numbers

---

## Common Test Cases

* Balanced numbers
* Highly unbalanced numbers
* Zero values
* Maximum constraint values

---

## Common Mistakes to Avoid

* Incrementing the largest instead of smallest
* Forgetting exactly 5 operations
* Incorrect comparison logic

---

## Interview Relevance

* Demonstrates greedy reasoning
* Tests understanding of product maximization
* Highlights balancing strategy

---

## What This Problem Teaches

* Product maximization principles
* Greedy decision making
* Effect of balancing in multiplicative systems

---

## Key Takeaways

* To maximize product under fixed increments, balance values.
* Incrementing the smallest element is optimal.
* Greedy works when local improvement guarantees global optimum.

---

## Problem Difficulty Analysis

This is an **Easy-level** Codeforces problem.

It tests mathematical intuition and greedy logic rather than complex algorithms, making it ideal for beginners and contest warm-ups.