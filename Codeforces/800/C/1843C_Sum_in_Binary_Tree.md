# C. Sum in Binary Tree

## Platform

Codeforces

## Problem Link

[C. Sum in Binary Tree - Codeforces Problem 1843C](https://codeforces.com/problemset/problem/1843/C?utm_source=chatgpt.com)

## Problem Statement

Consider an infinite complete binary tree where:

* The root is numbered `1`.
* For every node `x`:

  * Left child = `2x`
  * Right child = `2x + 1`

For each test case, you are given a node number `n`.

Starting from node `n`, repeatedly move to its parent until reaching the root.

Calculate the sum of all node values encountered on this path (including both `n` and the root).

## Input Format

* The first line contains an integer `t` — the number of test cases.
* Each of the next `t` lines contains a single integer `n`.

## Output Format

For each test case, print a single integer — the sum of all node values on the path from node `n` to the root.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 10^18`

## Examples

### Example 1

Input

```text
3
1
7
10
```

Output

```text
1
11
18
```

### Explanation

#### Test Case 1

Path:

```text
1
```

Sum:

```text
1
```

---

#### Test Case 2

Node:

```text
7
```

Parent sequence:

```text
7 → 3 → 1
```

Sum:

```text
7 + 3 + 1 = 11
```

Output:

```text
11
```

---

#### Test Case 3

Node:

```text
10
```

Parent sequence:

```text
10 → 5 → 2 → 1
```

Sum:

```text
10 + 5 + 2 + 1 = 18
```

Output:

```text
18
```

---

## Approach

### Algorithm Type

Binary Tree Parent Traversal (Bitwise Simulation)

## Intuition

In a complete binary tree numbered in this manner, the parent of a node is obtained by:

```text
parent = node / 2
```

Using integer division.

The solution repeatedly:

* Adds the current node value to the answer.
* Moves to its parent.

This continues until the root (`1`) is processed.

The given implementation performs the parent operation efficiently using a **right shift (`>>= 1`)**, which is equivalent to dividing by `2`.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read `n`.
  * Initialize:

```text
sum = n
```

* While `n > 0`:

  * Move to the parent:

```text
n >>= 1
```

```
* Add the parent value to `sum`.
```

* Print `sum`.

## Visual Walkthrough

### Test Case 1

Input:

```text
n = 7
```

Traversal:

```text
7
↓
3
↓
1
↓
0 (stop)
```

Accumulated sum:

```text
7
7 + 3 = 10
10 + 1 = 11
```

Answer:

```text
11
```

---

### Test Case 2

Input:

```text
n = 10
```

Traversal:

```text
10
↓
5
↓
2
↓
1
↓
0
```

Accumulated sum:

```text
10
15
17
18
```

Answer:

```text
18
```

---

### Test Case 3

Input:

```text
n = 1
```

Traversal:

```text
1
↓
0
```

Accumulated sum:

```text
1
```

Answer:

```text
1
```

## Complexity Analysis

### Time Complexity

Each iteration divides `n` by `2`.

Therefore, the number of iterations equals the height of the binary tree.

```text
Iterations = log₂(n)
```

Hence:

**Time Complexity = O(log n)**

---

### Space Complexity

Only two variables are maintained:

* `n`
* `sum`

No extra data structures are used.

Therefore:

**Space Complexity = O(1)**

## Solution Explanation

The solution relies on the numbering property of a complete binary tree.

For any node:

```text
Parent = floor(node / 2)
```

Instead of using division, the implementation performs:

```text
n >>= 1
```

which shifts the binary representation one bit to the right, producing the same result.

During every iteration:

* The current ancestor is added to the total.
* The traversal moves one level closer to the root.

Once the value becomes `0`, every ancestor has been processed and the accumulated sum is printed.

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

        // Given node in the binary tree
        long long n;
        cin >> n;

        // Initialize answer with the starting node
        long long sum = n;

        // Move towards the root by repeatedly finding the parent
        while(n > 0) {

            // Right shift by one is equivalent to dividing by 2
            // and moving to the parent node
            sum += (n >>= 1);
        }

        // Print the required sum
        cout << sum << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input `n` | Path to Root   | Sum | Output |
| --------- | -------------- | --- | ------ |
| 1         | 1              | 1   | 1      |
| 2         | 2 → 1          | 3   | 3      |
| 7         | 7 → 3 → 1      | 11  | 11     |
| 10        | 10 → 5 → 2 → 1 | 18  | 18     |
| 15        | 15 → 7 → 3 → 1 | 26  | 26     |

## Edge Cases to Consider

* Root node (`n = 1`)
* Powers of two (only left-child ancestors)
* Large values of `n`
* Odd node numbers
* Even node numbers

## Common Test Cases

### Root Node

```text
Input:
1
1

Output:
1
```

---

### Even Node

```text
Input:
1
10

Output:
18
```

---

### Odd Node

```text
Input:
1
7

Output:
11
```

---

### Large Value

```text
Input:
1
1024

Output:
2047
```

## Common Mistakes to Avoid

* Forgetting to include the starting node in the sum.
* Using floating-point division instead of integer division (or right shift) to find the parent.
* Stopping the traversal before adding the root node.

## Interview Relevance

* Demonstrates traversal using parent relationships in binary trees.
* Tests understanding of bitwise operations and their equivalence to arithmetic.
* Reinforces logarithmic-time algorithms based on repeated halving.

## What This Problem Teaches

* Parent traversal in complete binary trees.
* Efficient use of bitwise right shift for division by two.
* Solving tree problems without explicitly constructing the tree.

## Key Takeaways

* In a complete binary tree numbered level-wise, the parent of node `x` is `⌊x/2⌋`.
* Repeatedly dividing by two visits every ancestor up to the root.
* Bitwise operations provide an efficient and elegant implementation.
* The traversal requires only **O(log n)** time and **O(1)** extra space.

## Problem Difficulty Analysis

This is an **Easy** implementation and mathematics problem.

The crucial observation is that the parent of any node can be obtained by halving its value. Once this property is recognized, the solution becomes a straightforward logarithmic traversal from the given node to the root using repeated right shifts.