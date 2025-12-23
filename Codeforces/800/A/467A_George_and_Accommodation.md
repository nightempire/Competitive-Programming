# A. George and Accommodation

## Platform

Codeforces

## Problem Link

[A. George and Accommodation](https://codeforces.com/problemset/problem/467/A)

## Problem Statement

George wants to move into a new apartment.

There are `n` apartments.
For each apartment, you are given:

* `p` — the number of people currently living in the apartment
* `q` — the maximum capacity of the apartment

George wants to choose an apartment where **at least two more people** can move in without exceeding the apartment’s capacity.

Determine how many apartments satisfy this condition.

## Input Format

* The first line contains an integer `n`, the number of apartments
* The next `n` lines each contain two integers `p` and `q`

## Output Format

Print a single integer representing the number of suitable apartments.

## Constraints

* `1 ≤ n ≤ 100`
* `0 ≤ p < q ≤ 100`

## Examples

### Example 1

Input

```
3
1 3
2 3
3 3
```

Explanation

* Apartment 1: `3 - 1 = 2` → suitable
* Apartment 2: `3 - 2 = 1` → not suitable
* Apartment 3: `3 - 3 = 0` → not suitable

Output

```
1
```

### Example 2

Input

```
4
0 4
1 4
2 4
3 4
```

Explanation

Apartments with at least two free spaces are counted.

Output

```
2
```

## Approach

Simple conditional counting.

Each apartment is checked independently to see if it has room for at least two additional people.

## Intuition

The condition for an apartment to be suitable is:

```
capacity - living ≥ 2
```

If this condition is satisfied, the apartment is counted.

## Algorithm Steps

* Read integer `n`
* Initialize a counter variable
* For each apartment:

  * Read `living` and `capacity`
  * If `capacity - living ≥ 2`, increment the counter
* Output the counter

## Visual Walkthrough

Apartment data:

```
Living = 1, Capacity = 4
```

Free spaces:

```
4 - 1 = 3 ≥ 2 → suitable
```

Apartment is counted.

## Complexity Analysis

### Time Complexity

**O(n)**
Each apartment is processed once.

### Space Complexity

**O(1)**
Only constant extra variables are used.

## Solution Explanation

The solution iterates through all apartments and evaluates whether each one can accommodate at least two more people.

The expression `capacity - living - 2 >= 0` directly enforces the problem’s condition and ensures clarity in logic.

This approach is efficient, readable, and fully aligned with the problem requirements.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of apartments
    int n;

    // Counter for suitable apartments
    int count = 0;

    // Read number of apartments
    cin >> n;

    // Process each apartment
    while (n--) {

        int living, capacity;
        cin >> living >> capacity;

        // Check if at least two more people can move in
        if (capacity - living - 2 >= 0)
            count++;
    }

    // Output the result
    cout << count << endl;

    return 0;
}
```

## Test Cases Analysis

| Apartments | Living, Capacity | Expected Count |
| ---------: | ---------------- | -------------- |
|          1 | 0 2              | 1              |
|          3 | 1 3, 2 3, 3 3    | 1              |
|          4 | Mixed            | Valid count    |

## Edge Cases to Consider

* Apartments already full
* Apartments with exactly two free spaces
* Minimum number of apartments

## Common Test Cases

* All apartments suitable
* No apartment suitable
* Mixed availability

## Common Mistakes to Avoid

* Using `>` instead of `≥`
* Misinterpreting the problem condition
* Forgetting to reset or initialize the counter

## Interview Relevance

* Tests conditional logic
* Evaluates input handling
* Common filtering problem in interviews

## What This Problem Teaches

* Translating real-world constraints into conditions
* Simple arithmetic checks
* Efficient iteration

## Key Takeaways

* Clear conditions lead to simple solutions
* Avoid unnecessary complexity
* Always verify boundary conditions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It emphasizes straightforward condition checking and is well-suited for beginners and interview warm-up practice.
