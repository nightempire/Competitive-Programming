# B_Increasing

## Platform

Codeforces

## Problem Link

[B. Increasing](https://codeforces.com/problemset/problem/1660/B)

## Problem Statement

You are given multiple test cases.
For each test case, an integer `n` is provided followed by `n` integers.

Your task is to determine whether the given sequence can be considered **strictly increasing in terms of distinct values**.
In other words, the array should **not contain any duplicate elements**.

If all elements in the array are unique, print `YES`.
Otherwise, print `NO`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`, the size of the array.
  * The second line contains `n` integers representing the array elements.

## Output Format

For each test case, print:

* `YES` — if all elements are distinct
* `NO` — if at least one duplicate element exists

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 2 × 10^5`
* `1 ≤ array[i] ≤ 10^9`
* The sum of `n` over all test cases does not exceed `2 × 10^5`

## Examples

### Example 1

Input

```
2
5
1 2 3 4 5
4
1 2 2 3
```

Explanation

* Test case 1: All elements are unique → valid
* Test case 2: Element `2` appears more than once → invalid

Output

```
YES
NO
```

### Example 2

Input

```
1
3
7 7 7
```

Explanation

* All elements are the same, so duplicates exist

Output

```
NO
```

## Approach

**Hashing / Set-based Uniqueness Check**

The problem is solved by leveraging a hash-based data structure to track whether an element has already appeared.

## Intuition

A strictly increasing sequence cannot contain duplicate values.
If even one number appears more than once, the condition fails immediately.

Using a hash set allows us to:

* Insert elements efficiently
* Detect duplicates in constant average time

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read `n`.
  * Initialize an empty hash set.
  * Initialize a boolean flag to track duplicates.
  * For each of the `n` numbers:

    * Attempt to insert the number into the set.
    * If insertion fails, a duplicate exists:

      * Mark the flag.
  * Print `NO` if a duplicate was found, otherwise print `YES`.

## Visual Walkthrough

### Test Case 1

Input

```
1 2 3 4
```

Set evolution:

```
{}
{1}
{1, 2}
{1, 2, 3}
{1, 2, 3, 4}
```

All insertions succeed → `YES`

---

### Test Case 2

Input

```
3 5 3 7
```

Set evolution:

```
{}
{3}
{3, 5}
Attempt to insert 3 → already exists
```

Duplicate detected → `NO`

---

### Test Case 3

Input

```
9
```

Set evolution:

```
{}
{9}
```

Single element → always valid → `YES`

## Complexity Analysis

### Time Complexity

**O(n) per test case**

Each insertion and lookup in the hash set takes constant average time.
All elements are processed exactly once.

### Space Complexity

**O(n)**

In the worst case, all elements are unique and stored in the hash set.

## Solution Explanation

The solution efficiently checks for duplicate elements using a hash set.
As soon as a duplicate is detected, the result for that test case is determined.
This avoids unnecessary processing and ensures optimal performance within constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <unordered_set>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Size of the array
        int n;
        cin >> n;

        // Hash set to store unique elements
        unordered_set<int> seen;

        // Flag to indicate if a duplicate is found
        bool hasDuplicate = false;

        // Read all elements of the array
        for (int i = 0; i < n; i++) {

            int value;
            cin >> value;

            /*
             Attempt to insert the value into the set.
             insert() returns a pair:
             - first  -> iterator
             - second -> true if insertion succeeded, false if value already exists
            */
            if (!hasDuplicate && !seen.insert(value).second) {
                // Duplicate detected
                hasDuplicate = true;
            }
        }

        // Output result based on whether a duplicate was found
        cout << (hasDuplicate ? "NO\n" : "YES\n");
    }

    return 0;
}
```

## Test Cases Analysis

| Test Case | Input Array        | Duplicate Exists | Output |
| --------- | ------------------ | ---------------- | ------ |
| 1         | 1 2 3 4            | No               | YES    |
| 2         | 1 2 2 3            | Yes              | NO     |
| 3         | 5                  | No               | YES    |
| 4         | 7 7 7              | Yes              | NO     |
| 5         | Large unique array | No               | YES    |

## Edge Cases to Consider

* Array of size `1`
* All elements are the same
* Large input size with all unique elements
* Duplicate appearing at the very end of the array

## Common Test Cases

* Strictly increasing numbers
* Random order with unique values
* Single duplicate among large data
* Fully duplicated array

## Common Mistakes to Avoid

* Using sorting when only uniqueness is required
* Forgetting to reset data structures between test cases
* Ignoring early detection of duplicates

## Interview Relevance

* Demonstrates understanding of hashing
* Tests knowledge of STL containers
* Evaluates time and space optimization skills

## What This Problem Teaches

* Efficient duplicate detection
* Practical use of hash sets
* Early termination logic in problem solving

## Key Takeaways

* Uniqueness checks are best handled using hash-based structures
* Avoid unnecessary sorting when not required
* Clean logic improves both performance and readability

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on fundamental data structures and is commonly used to assess basic problem-solving and STL proficiency.