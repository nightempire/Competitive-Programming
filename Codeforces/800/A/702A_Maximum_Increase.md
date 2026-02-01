# A_Maximum_Increase

## Platform

Codeforces

## Problem Link

[A. Maximum Increase](https://codeforces.com/problemset/problem/702/A)

## Problem Statement

You are given an integer array of size `n`.

Your task is to determine the **maximum length of a contiguous strictly increasing subarray**.

A subarray is considered **strictly increasing** if each element is **greater than the previous one**.

## Input Format

* The first line contains an integer `n` — the size of the array.
* The second line contains `n` integers representing the array elements.

## Output Format

* Print a single integer — the maximum length of a contiguous strictly increasing subarray.

## Constraints

* `1 ≤ n ≤ 10⁵`
* `1 ≤ array[i] ≤ 10⁹`

## Examples

### Example 1

Input

```
5
1 2 2 4 5
```

Explanation

* Increasing subarrays:

  * `[1, 2]` → length 2
  * `[2]` → length 1
  * `[2, 4, 5]` → length 3

Maximum length:

```
3
```

Output

```
3
```

---

### Example 2

Input

```
6
1 2 3 4 5 6
```

Explanation
The entire array is strictly increasing.

Output

```
6
```

---

### Example 3

Input

```
4
5 4 3 2
```

Explanation
No two consecutive elements form an increasing sequence.

Output

```
1
```

## Approach

Single-pass greedy scan with running length tracking.

## Intuition

A strictly increasing subarray grows as long as the current element is greater than the previous one.

* If the sequence continues increasing, extend the current length.
* If the increase breaks, reset the length to `1`.
* Track the maximum length encountered during the traversal.

This allows solving the problem in one pass without extra space.

## Algorithm Steps

* Read `n`
* Read the first element and initialize:

  * `len = 1` for current increasing sequence length
  * `maxi = 1` for maximum length found
* For each subsequent element:

  * If the current element is greater than the previous:

    * Increment `len`
    * Update `maxi` if needed
  * Otherwise:

    * Reset `len` to `1`
  * Update `prev` to the current element
* Print `maxi`

## Visual Walkthrough

### Case 1

```
Array: [1, 2, 2, 4, 5]
```

Tracking:

```
1 → 2   (increase, len = 2)
2 → 2   (break, len = 1)
2 → 4   (increase, len = 2)
4 → 5   (increase, len = 3)
```

Maximum length:

```
3
```

---

### Case 2

```
Array: [5, 4, 3, 2]
```

Each step breaks the increase.

Maximum length:

```
1
```

---

### Case 3

```
Array: [1, 3, 5, 7]
```

Sequence always increases.

Maximum length:

```
4
```

## Complexity Analysis

### Time Complexity

**O(n)**

Each element is processed exactly once.

### Space Complexity

**O(1)**

Only constant extra variables are used.

## Solution Explanation

The solution maintains the length of the current increasing subarray and updates the maximum length whenever a longer increasing segment is found.
When the increasing condition fails, the current length is reset.
This greedy, linear approach efficiently finds the answer without additional memory.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of elements in the array
    int n;
    cin >> n;

    // Variable to store the previous element
    int prev = 0;

    // Length of the current increasing subarray
    int len = 1;

    // Maximum length found so far
    int maxi = 1;

    // Read the first element
    cin >> prev;

    // Iterate through the remaining elements
    for(int i = 1; i < n; i++) {

        int curr;
        cin >> curr;

        // If the current element is greater than the previous,
        // the increasing sequence continues
        if(curr > prev) {

            // Increase the current length
            if(++len > maxi)
                maxi++;
        }
        else {
            // Reset length if the sequence breaks
            len = 1;
        }

        // Update previous element
        prev = curr;
    }

    // Output the maximum increasing subarray length
    cout << maxi;

    return 0;
}
```

## Test Cases Analysis

| Input Array     | Longest Increasing Segment | Output |
| --------------- | -------------------------- | ------ |
| `[1,2,2,4,5]`   | `[2,4,5]`                  | `3`    |
| `[1,2,3,4,5,6]` | Entire array               | `6`    |
| `[5,4,3,2]`     | Any single element         | `1`    |
| `[3,3,3]`       | Any single element         | `1`    |

## Edge Cases to Consider

* Array of size `1`
* All elements equal
* Strictly decreasing array

## Common Test Cases

* Fully increasing array
* Mixed increasing and decreasing segments
* Repeated values breaking increase

## Common Mistakes to Avoid

* Forgetting to reset length when increase breaks
* Comparing with `>=` instead of `>`
* Not initializing the first element correctly

## Interview Relevance

* Tests array traversal skills
* Evaluates greedy reasoning
* Common sliding-window style pattern

## What This Problem Teaches

* Efficient single-pass scanning
* Handling contiguous subarrays
* Maintaining running state variables

## Key Takeaways

* Greedy approaches can simplify contiguous sequence problems
* Always track both current state and global best
* One-pass solutions are often optimal for array scans

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic array traversal and condition checking, making it a common introductory problem for competitive programming and technical interviews.