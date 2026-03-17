# A_Robin_Helps

## Platform

Codeforces

## Problem Link

[A. Robin Helps](https://codeforces.com/problemset/problem/2014/A)

## Problem Statement

Robin is helping people by distributing gold.

You are given a sequence of `n` integers:

* If the value is **greater than or equal to `k`**, Robin gains that amount of gold.
* If the value is `0`, a person asks for help:

  * If Robin has at least **1 gold**, he gives **1 gold** and helps the person.
  * Otherwise, he cannot help.

Your task is to determine **how many people Robin can help**.

## Input Format

* The first line contains an integer `t` — the number of test cases.
* For each test case:

  * The first line contains two integers `n` and `k`.
  * The second line contains `n` integers.

## Output Format

For each test case, print a single integer — the number of people Robin helps.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 100`
* `1 ≤ k ≤ 100`
* `0 ≤ ai ≤ 100`

## Examples

### Example 1

Input

```
1
6 5
5 0 10 0 0 3
```

Explanation

Step-by-step:

| Value | Action       | Gold | Help Count |
| ----- | ------------ | ---- | ---------- |
| 5     | Gain gold    | 5    | 0          |
| 0     | Help (use 1) | 4    | 1          |
| 10    | Gain gold    | 14   | 1          |
| 0     | Help         | 13   | 2          |
| 0     | Help         | 12   | 3          |
| 3     | Ignore (< k) | 12   | 3          |

Output

```
3
```

---

### Example 2

Input

```
1
5 4
0 0 4 0 0
```

Explanation

| Value | Action                | Gold | Help Count |
| ----- | --------------------- | ---- | ---------- |
| 0     | No gold → cannot help | 0    | 0          |
| 0     | No gold → cannot help | 0    | 0          |
| 4     | Gain gold             | 4    | 0          |
| 0     | Help                  | 3    | 1          |
| 0     | Help                  | 2    | 2          |

Output

```
2
```

---

### Example 3

Input

```
1
4 3
3 3 0 0
```

Explanation

| Value | Action    | Gold | Help Count |
| ----- | --------- | ---- | ---------- |
| 3     | Gain gold | 3    | 0          |
| 3     | Gain gold | 6    | 0          |
| 0     | Help      | 5    | 1          |
| 0     | Help      | 4    | 2          |

Output

```
2
```

## Approach

Greedy Simulation with Resource Tracking

## Intuition

We maintain a variable:

```
gold = total gold Robin currently has
```

Rules:

* If `ai ≥ k` → Robin gains gold.
* If `ai == 0`:

  * If `gold > 0` → help (consume 1 gold)
  * Otherwise → cannot help

We process the sequence **from left to right**, always using available gold greedily to help when possible.

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read `n`, `k`.
  * Initialize:

    * `gold = 0`
    * `count = 0`
  * For each element:

    * If `num ≥ k`:

      * `gold += num`
    * Else if `num == 0`:

      * If `gold > 0`:

        * `gold--`
        * `count++`
  * Print `count`.

## Visual Walkthrough

### Test Case 1

Input

```
5 0 10 0 0 3
k = 5
```

Steps:

```
gold = 0

5  → gold = 5
0  → help → gold = 4, count = 1
10 → gold = 14
0  → help → gold = 13, count = 2
0  → help → gold = 12, count = 3
3  → ignored
```

Result:

```
3
```

---

### Test Case 2

```
0 0 4 0 0
k = 4
```

Steps:

```
gold = 0

0 → no help
0 → no help
4 → gold = 4
0 → help → gold = 3, count = 1
0 → help → gold = 2, count = 2
```

Result:

```
2
```

---

### Test Case 3

```
3 3 0 0
k = 3
```

Steps:

```
gold = 0

3 → gold = 3
3 → gold = 6
0 → help → gold = 5, count = 1
0 → help → gold = 4, count = 2
```

Result:

```
2
```

## Complexity Analysis

### Time Complexity

```
O(n) per test case
```

Each element is processed once.

### Space Complexity

```
O(1)
```

Only constant variables are used.

## Solution Explanation

The program simulates Robin’s actions:

* Collect gold whenever possible (`ai ≥ k`)
* Use gold greedily to help when encountering `0`

This ensures maximum number of people helped because:

* Helping earlier does not reduce future opportunities unnecessarily.
* Gold is only spent when needed.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t, n, k;
    cin >> t;

    while(t--) {

        cin >> n >> k;

        // Current gold Robin has
        int gold = 0;

        // Number of people helped
        int count = 0;

        for(int i = 0; i < n; i++) {

            int num;
            cin >> num;

            // If value is >= k, gain gold
            if(num >= k) {
                gold += num;
            }

            // If someone needs help (value = 0)
            else if(num == 0 && gold > 0) {
                count++;
                gold--;
            }
        }

        // Output number of people helped
        cout << count << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input Array  | k | Gold Flow          | Help Count |
| ------------ | - | ------------------ | ---------- |
| 5 0 10 0 0 3 | 5 | Accumulated → Used | 3          |
| 0 0 4 0 0    | 4 | Late gain          | 2          |
| 3 3 0 0      | 3 | Early accumulation | 2          |

## Edge Cases to Consider

* All elements are `0`
* No element ≥ `k`
* All elements ≥ `k`
* Single element array

## Common Test Cases

```
0 0 0 0
5 5 5 5
1 2 3 4
10 0 10 0
```

## Common Mistakes to Avoid

* Helping when `gold == 0`
* Ignoring condition `num ≥ k`
* Misinterpreting values `< k` but not `0`

## Interview Relevance

* Demonstrates greedy resource management
* Tests simulation skills
* Reinforces conditional logic

## What This Problem Teaches

* Efficient simulation of processes
* Resource allocation strategies
* Greedy decision making

## Key Takeaways

* Always track available resources
* Use greedy approach when local optimal decisions are safe
* Simple simulation often solves real-world modeled problems

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It involves straightforward simulation with conditional logic and is ideal for beginners to practice greedy strategies.