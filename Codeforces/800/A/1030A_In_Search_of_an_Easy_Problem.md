# A. In Search of an Easy Problem

## Platform

Codeforces

## Problem Link

[A. In Search of an Easy Problem](https://codeforces.com/problemset/problem/1030/A)

## Problem Statement

You are given opinions of `n` people about a problem.

Each person states:

* `0` — the problem is easy
* `1` — the problem is hard

If **at least one person** thinks the problem is hard, then the problem is considered **hard**.
Otherwise, it is considered **easy**.

Determine whether the problem is `"EASY"` or `"HARD"`.

## Input Format

* The first line contains an integer `n`, the number of people
* The second line contains `n` integers (`0` or `1`) representing their opinions

## Output Format

Print `"EASY"` if the problem is easy, otherwise print `"HARD"`.

## Constraints

* `1 ≤ n ≤ 100`
* Each opinion is either `0` or `1`

## Examples

### Example 1

Input

```
3
0 0 0
```

Explanation

All participants think the problem is easy.

Output

```
EASY
```

### Example 2

Input

```
4
0 1 0 0
```

Explanation

At least one participant thinks the problem is hard.

Output

```
HARD
```

## Approach

Flag-based detection during input processing.

## Intuition

The condition is simple:
the presence of **any** `1` immediately determines the result.

There is no need to count all opinions; a single hard opinion is sufficient.

## Algorithm Steps

* Read integer `n`
* Initialize a flag variable to indicate hardness
* For each opinion:

  * If the opinion is `1`, set the flag
* After processing all opinions:

  * Print `"HARD"` if the flag is set
  * Otherwise, print `"EASY"`

## Visual Walkthrough

Input opinions:

```
0 1 0
```

Processing:

```
Read 0 → still easy
Read 1 → flag set (hard)
Read 0 → no change
```

Final decision:

```
HARD
```

## Complexity Analysis

### Time Complexity

**O(n)**
Each opinion is read once.

### Space Complexity

**O(1)**
Only constant extra variables are used.

## Solution Explanation

The solution reads each opinion one by one.

If a `1` is encountered, a flag is set to indicate that at least one person finds the problem hard.
After all inputs are processed, the final decision is based solely on the value of this flag.

This approach is efficient and aligns perfectly with the problem requirements.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of people
    int n;

    // Flag to indicate if any opinion is hard
    int flag = 0;

    // Read number of people
    cin >> n;

    // Process opinions
    while (n--) {

        int opinion;
        cin >> opinion;

        // If any opinion is hard, set the flag
        if (opinion == 1)
            flag = 1;
    }

    // Output result based on flag
    cout << (flag ? "HARD" : "EASY") << endl;

    return 0;
}
```

## Test Cases Analysis

| n | Opinions  | Output |
| - | --------- | ------ |
| 1 | 0         | EASY   |
| 1 | 1         | HARD   |
| 3 | 0 0 0     | EASY   |
| 5 | 0 0 1 0 0 | HARD   |

## Edge Cases to Consider

* Only one participant
* First opinion is hard
* Last opinion is hard

## Common Test Cases

* All opinions are `0`
* Exactly one `1` among zeros
* Multiple `1`s

## Common Mistakes to Avoid

* Counting all opinions unnecessarily
* Printing result before processing all inputs
* Misinterpreting `0` and `1`

## Interview Relevance

* Tests understanding of early decision logic
* Evaluates efficient input handling
* Common beginner-level screening problem

## What This Problem Teaches

* Short-circuit logic
* Efficient condition checking
* Clean and minimal code structure

## Key Takeaways

* Sometimes a single condition decides the outcome
* Avoid overcomplicating simple logic
* Early detection improves clarity

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic input processing and conditional checks, making it ideal for beginners and quick interview assessments.
