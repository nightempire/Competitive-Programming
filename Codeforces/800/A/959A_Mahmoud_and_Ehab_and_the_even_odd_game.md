# A. Mahmoud and Ehab and the Even-Odd Game

## Platform

Codeforces

## Problem Link

[A. Mahmoud and Ehab and the Even-Odd Game](https://codeforces.com/problemset/problem/959/A)

## Problem Statement

Mahmoud and Ehab are playing a simple game.

They are given a single integer `n`.

The rules of the game are:

* If `n` is **even**, Mahmoud wins.
* If `n` is **odd**, Ehab wins.

Your task is to determine the winner of the game based on the value of `n`.

## Input Format

* A single integer `n`.

## Output Format

* Print `"Mahmoud"` if `n` is even.
* Print `"Ehab"` if `n` is odd.

## Constraints

* `1 ≤ n ≤ 10⁹`

## Examples

### Example 1

Input

```
1
```

Explanation

`1` is odd, so Ehab wins.

Output

```
Ehab
```

---

### Example 2

Input

```
4
```

Explanation

`4` is even, so Mahmoud wins.

Output

```
Mahmoud
```

---

### Example 3

Input

```
7
```

Explanation

`7` is odd.

Output

```
Ehab
```

## Approach

**Parity check using bitwise operation**

## Intuition

The game outcome depends entirely on whether the given number is **even or odd**.

A number is odd if its **least significant bit is set**.
Using a bitwise AND operation with `1` allows this check efficiently.

## Algorithm Steps

* Read the integer `n`.
* Check the parity of `n`:

  * If `n` is odd, print `"Ehab"`.
  * Otherwise, print `"Mahmoud"`.

## Visual Walkthrough

### Case 1

```
n = 1
Binary: 0001
LSB = 1 → Odd
Winner: Ehab
```

---

### Case 2

```
n = 4
Binary: 0100
LSB = 0 → Even
Winner: Mahmoud
```

---

### Case 3

```
n = 7
Binary: 0111
LSB = 1 → Odd
Winner: Ehab
```

## Complexity Analysis

### Time Complexity

**O(1)**

Only a single parity check is performed.

### Space Complexity

**O(1)**

No extra space is used.

## Solution Explanation

The solution relies on the fact that the parity of a number determines the winner.

Using the bitwise expression `n & 1`:

* If the result is `1`, the number is odd → Ehab wins.
* If the result is `0`, the number is even → Mahmoud wins.

This makes the solution both concise and efficient.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Read the number
    int n;
    cin >> n;

    // If n is odd, Ehab wins; otherwise, Mahmoud wins
    cout << (n & 1 ? "Ehab" : "Mahmoud");

    return 0;
}
```

## Test Cases Analysis

| Input | Parity | Output  |
| ----- | ------ | ------- |
| 1     | Odd    | Ehab    |
| 2     | Even   | Mahmoud |
| 7     | Odd    | Ehab    |
| 10    | Even   | Mahmoud |

## Edge Cases to Consider

* Minimum value (`n = 1`)
* Very large even number
* Very large odd number

## Common Test Cases

* Small odd number
* Small even number
* Boundary values

## Common Mistakes to Avoid

* Reversing the winner conditions
* Using unnecessary loops or conditions
* Incorrect output spelling

## Interview Relevance

* Tests understanding of parity
* Demonstrates bitwise operations
* Simple logic-based decision making

## What This Problem Teaches

* Even–odd checks using bitwise operators
* Mapping problem rules directly to code
* Writing concise and readable logic

## Key Takeaways

* Parity problems can often be solved in one line
* Bitwise checks are fast and reliable
* Always match output exactly as required

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic conditional logic and parity checking, making it suitable for beginners and quick interview warm-up questions.