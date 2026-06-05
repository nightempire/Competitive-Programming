## 2033A. Sakurako and Kosuke

## Platform

Codeforces

## Problem Link

[A. Sakurako and Kosuke](https://codeforces.com/problemset/problem/2033/A)

## Problem Statement

Sakurako and Kosuke are playing a game involving a single integer `n`.

Both players play optimally, and the winner depends entirely on the parity of `n`.

Determine who wins the game for each test case.

The winning condition is:

* If `n` is odd, **Kosuke** wins.
* If `n` is even, **Sakurako** wins.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains a single integer `n`.

## Output Format

For each test case, print:

* `"Kosuke"` if Kosuke wins.
* `"Sakurako"` if Sakurako wins.

## Constraints

* `1 ≤ t ≤ 10^4`
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

Explanation

```text
n = 1 → odd  → Kosuke wins
n = 2 → even → Sakurako wins
n = 5 → odd  → Kosuke wins
```

Output

```text
Kosuke
Sakurako
Kosuke
```

---

### Example 2

Input

```text
4
4
7
10
13
```

Explanation

```text
4  → even → Sakurako
7  → odd  → Kosuke
10 → even → Sakurako
13 → odd  → Kosuke
```

Output

```text
Sakurako
Kosuke
Sakurako
Kosuke
```

---

### Example 3

Input

```text
2
100
101
```

Explanation

```text
100 → even → Sakurako
101 → odd  → Kosuke
```

Output

```text
Sakurako
Kosuke
```

## Approach

Parity Check (Game Theory Observation)

## Intuition

The game's outcome depends solely on whether `n` is odd or even.

Observation:

* Odd numbers are winning positions for **Kosuke**.
* Even numbers are winning positions for **Sakurako**.

Therefore, we only need to determine the parity of `n`.

A number is:

```text
Odd  → n & 1 = 1
Even → n & 1 = 0
```

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read `n`.

  * Check parity using:

    ```text
    n & 1
    ```

  * If odd:

    ```text
    Kosuke
    ```

  * Otherwise:

    ```text
    Sakurako
    ```

## Visual Walkthrough

### Case 1

```text
n = 1
```

Parity:

```text
1 & 1 = 1
```

Result:

```text
Kosuke
```

---

### Case 2

```text
n = 8
```

Parity:

```text
8 & 1 = 0
```

Result:

```text
Sakurako
```

---

### Case 3

```text
n = 15
```

Parity:

```text
15 & 1 = 1
```

Result:

```text
Kosuke
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case

Only a single parity check is performed.

### Space Complexity

**O(1)**

No additional data structures are used.

## Solution Explanation

The solution uses a simple bitwise operation:

```cpp
n & 1
```

This determines whether the least significant bit is set.

* If set (`1`), the number is odd, so **Kosuke** wins.
* Otherwise, the number is even, so **Sakurako** wins.

Since no simulation or recursion is required, the solution is extremely efficient.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Input value
        int n;
        cin >> n;

        // Odd number -> Kosuke wins
        // Even number -> Sakurako wins
        cout << (n & 1 ? "Kosuke\n" : "Sakurako\n");
    }

    return 0;
}
```

## Test Cases Analysis

| n  | Parity | Winner   |
| -- | ------ | -------- |
| 1  | Odd    | Kosuke   |
| 2  | Even   | Sakurako |
| 5  | Odd    | Kosuke   |
| 8  | Even   | Sakurako |
| 15 | Odd    | Kosuke   |

## Edge Cases to Consider

* Minimum value `n = 1`
* Large odd values
* Large even values
* Consecutive odd/even numbers

## Common Test Cases

* `n = 1`
* `n = 2`
* `n = 99`
* `n = 100`
* `n = 1000000000`

## Common Mistakes to Avoid

* Reversing the winners for odd and even values.
* Using unnecessary game simulation.
* Forgetting that parity alone determines the result.

## Interview Relevance

* Tests understanding of parity.
* Demonstrates efficient use of bitwise operators.
* Highlights observation-based problem solving.

## What This Problem Teaches

* Using parity to solve game theory problems.
* Recognizing when a complex-looking game reduces to a simple pattern.
* Applying bitwise operations for fast checks.

## Key Takeaways

* Many game problems have simple parity-based solutions.
* Bitwise operations provide an efficient way to check odd/even status.
* Always look for patterns before attempting simulation.

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The challenge is identifying the parity pattern governing the winner. Once observed, the implementation requires only a single bitwise check per test case.