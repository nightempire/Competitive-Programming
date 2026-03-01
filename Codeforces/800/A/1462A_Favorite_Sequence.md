# A_Favorite_Sequence

## Platform

Codeforces

## Problem Link

[A. Favorite Sequence](https://codeforces.com/problemset/problem/1462/A)

---

## Problem Statement

You are given a sequence of `n` integers.

You need to rearrange the sequence in the following manner:

* First element
* Last element
* Second element
* Second last element
* Third element
* Third last element
* … and so on

Print the resulting sequence.

---

## Input Format

* The first line contains an integer `t` — number of test cases.
* For each test case:

  * An integer `n`
  * A sequence of `n` integers

---

## Output Format

For each test case, print the rearranged sequence.

---

## Constraints

* `1 ≤ t ≤ 100`
* `1 ≤ n ≤ 100`
* `1 ≤ ai ≤ 1000`

---

## Examples

### Example 1

Input

```
1
6
1 2 3 4 5 6
```

Explanation

Original:

```
1 2 3 4 5 6
```

Rearranged:

```
1 6 2 5 3 4
```

Output

```
1 6 2 5 3 4
```

---

### Example 2

Input

```
1
5
10 20 30 40 50
```

Explanation

Original:

```
10 20 30 40 50
```

Rearranged:

```
10 50 20 40 30
```

Output

```
10 50 20 40 30
```

---

## Approach (Algorithm Type)

**Two-Pointer Technique (Bidirectional Traversal)**

---

## Intuition

We need to alternate elements from:

* Start of the array
* End of the array

This suggests maintaining two indices:

* `left = 0`
* `right = n - 1`

Then:

* Print `nums[left]`
* Print `nums[right]`
* Move `left++`
* Move `right--`

Continue until pointers meet.

If `n` is odd:

* One element remains in the middle.
* Print it at the end.

---

## Algorithm Steps

* Read integer `t`.
* For each test case:

  * Read `n`.
  * Store the array.
  * Initialize:

    ```
    left = 0
    right = n - 1
    ```
  * While `left < right`:

    * Print `nums[left]`
    * Print `nums[right]`
    * Increment `left`
    * Decrement `right`
  * If `left == right`:

    * Print middle element
  * Print newline.

---

## Visual Walkthrough

### Test Case 1

Input:

```
1 2 3 4 5 6
```

| Step | left | right | Output So Far |
| ---- | ---- | ----- | ------------- |
| 1    | 0    | 5     | 1 6           |
| 2    | 1    | 4     | 1 6 2 5       |
| 3    | 2    | 3     | 1 6 2 5 3 4   |

Final:

```
1 6 2 5 3 4
```

---

### Test Case 2

Input:

```
10 20 30 40 50
```

| Step | left | right | Output So Far  |
| ---- | ---- | ----- | -------------- |
| 1    | 0    | 4     | 10 50          |
| 2    | 1    | 3     | 10 50 20 40    |
| 3    | 2    | 2     | 10 50 20 40 30 |

Final:

```
10 50 20 40 30
```

---

### Test Case 3

Input:

```
7 8 9
```

Process:

```
7 9 8
```

---

## Complexity Analysis

### Time Complexity

For each test case:

* Reading array → O(n)
* Two-pointer traversal → O(n)

Overall:

```
O(n) per test case
```

---

### Space Complexity

```
O(n)
```

Array storage required.

---

## Solution Explanation

The solution:

* Stores the sequence.
* Uses two pointers:

  * One from beginning.
  * One from end.
* Alternately prints elements.
* Handles odd-length case separately.

This ensures correct reordering in linear time.

---

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

        int n;
        cin >> n;

        int nums[n];

        // Read input array
        for(int i = 0; i < n; i++) {
            cin >> nums[i];
        }

        int left = 0;
        int right = n - 1;

        // Alternate between left and right
        while(left < right) {
            cout << nums[left++] << ' ';
            cout << nums[right--] << ' ';
        }

        // If odd length, print middle element
        if(left == right) {
            cout << nums[left];
        }

        cout << '\n';
    }

    return 0;
}
```

---

## Test Cases Analysis

| Input          | Output         |
| -------------- | -------------- |
| 1 2 3 4 5 6    | 1 6 2 5 3 4    |
| 10 20 30 40 50 | 10 50 20 40 30 |
| 7 8 9          | 7 9 8          |
| 1              | 1              |

---

## Edge Cases to Consider

* `n = 1`
* `n = 2`
* Odd length arrays
* Even length arrays

---

## Common Test Cases

* Small arrays
* Maximum allowed size
* Repeated numbers
* Increasing sequence

---

## Common Mistakes to Avoid

* Forgetting to handle odd middle element
* Incorrect pointer updates
* Extra spaces formatting issues

---

## Interview Relevance

* Tests two-pointer pattern
* Reinforces array traversal techniques
* Simple but important pattern recognition

---

## What This Problem Teaches

* Two-pointer technique
* Pattern-based array rearrangement
* Handling boundary conditions

---

## Key Takeaways

* Two pointers efficiently solve alternating selection problems.
* Always check odd-length conditions.
* Linear traversal is sufficient.

---

## Problem Difficulty Analysis

This is an **Easy-level** Codeforces problem.

It mainly tests array manipulation and pointer logic, making it suitable for beginners and contest practice.