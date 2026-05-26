## 2162A. Beautiful Average

## Platform

Codeforces

## Problem Link

[Beautiful Average](https://codeforces.com/problemset/problem/2162/A)

## Problem Statement

You are given an array of integers.

Your task is to determine the maximum element in the array, which represents the answer for constructing the required beautiful average condition.

For each test case, output the maximum value present in the array.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * The first line contains an integer `n`, the size of the array.
  * The second line contains `n` integers.

## Output Format

* For each test case, print a single integer — the maximum element of the array.

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ n ≤ 100`
* `0 ≤ a[i] ≤ 10^9`

## Examples

### Example 1

Input

```id="yz89tw"
2
5
1 3 2 5 4
3
7 1 6
```

Explanation

* Maximum of `[1, 3, 2, 5, 4]` is `5`
* Maximum of `[7, 1, 6]` is `7`

Output

```id="zxv5k2"
5
7
```

---

### Example 2

Input

```id="t2j4rs"
1
4
9 9 9 9
```

Explanation

All elements are equal, so maximum is `9`.

Output

```id="x4bn9v"
9
```

---

### Example 3

Input

```id="h3y1gm"
1
6
0 2 8 1 5 3
```

Explanation

Largest value in the array is `8`.

Output

```id="m7jq0r"
8
```

## Approach

Linear Traversal (Maximum Element Search)

## Intuition

The problem reduces to finding the largest element in the array.

By scanning the array once and maintaining the current maximum value, we can efficiently determine the answer.

## Algorithm Steps

* Read number of test cases `t`
* For each test case:

  * Read integer `n`
  * Initialize `maxi = 0`
  * Traverse all array elements:

    * If current element is greater than `maxi`, update `maxi`
  * Print `maxi`

## Visual Walkthrough

### Case 1

```id="7xj3nt"
Array = [1, 3, 2, 5, 4]
```

```id="m9l0qp"
Current maximum progression:
1 → 3 → 3 → 5 → 5

Final answer = 5
```

---

### Case 2

```id="p6v5yx"
Array = [7, 1, 6]
```

```id="u4r8cm"
Current maximum progression:
7 → 7 → 7

Final answer = 7
```

---

### Case 3

```id="q3s8lk"
Array = [9, 9, 9, 9]
```

```id="f2h4vy"
All elements equal

Maximum = 9
```

## Complexity Analysis

### Time Complexity

**O(n) per test case**

Each element is visited exactly once.

### Space Complexity

**O(1)**

Only a single variable is used to track the maximum value.

## Solution Explanation

The solution iterates through the array and continuously updates the maximum element encountered so far. Since every element is checked exactly once, the approach is both simple and efficient.

## Full Solution

### C++ Implementation

```cpp id="n8y2qd"
#include<iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    while(t--) {

        // Size of array
        int n;

        // Variable to store maximum value
        int maxi = 0;

        cin >> n;

        int num;

        // Read all elements
        for(int i = 0; i < n; i++) {

            cin >> num;

            // Update maximum if current number is larger
            if(num > maxi) {
                maxi = num;
            }
        }

        // Print final maximum value
        cout << maxi << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Array         | Maximum Element | Output |
| ------------- | --------------- | ------ |
| [1,3,2,5,4]   | 5               | 5      |
| [7,1,6]       | 7               | 7      |
| [9,9,9,9]     | 9               | 9      |
| [0,2,8,1,5,3] | 8               | 8      |

## Edge Cases to Consider

* Single element array
* All elements equal
* Array containing zero
* Very large values

## Common Test Cases

* Strictly increasing arrays
* Strictly decreasing arrays
* Arrays with repeated maximum values
* Random unordered arrays

## Common Mistakes to Avoid

* Forgetting to initialize maximum properly
* Updating maximum incorrectly
* Using sorting unnecessarily

## Interview Relevance

* Basic array traversal problem
* Tests understanding of linear scans
* Common warm-up coding question

## What This Problem Teaches

* Efficient maximum searching
* Single-pass traversal techniques
* Avoiding unnecessary sorting

## Key Takeaways

* Finding maximum does not require sorting
* Linear traversal is optimal
* Maintain running state during iteration

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The implementation is straightforward and primarily tests basic array traversal and conditional logic.