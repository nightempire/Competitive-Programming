## 3300. Minimum Element After Replacement With Digit Sum

## Platform

LeetCode

## Problem Link

[Minimum Element After Replacement With Digit Sum](https://leetcode.com/problems/minimum-element-after-replacement-with-digit-sum/)

## Problem Statement

You are given an integer array `nums`.

Replace each element in the array with the **sum of its digits**. After performing all replacements, return the **minimum element** in the resulting array.

## Input Format

* An integer array `nums`

## Output Format

* Return an integer representing the minimum element after all replacements.

## Constraints

* `1 ≤ nums.length ≤ 100`
* `1 ≤ nums[i] ≤ 10^4`

## Examples

### Example 1

Input

```text
nums = [10,12,13,14]
```

Explanation

Digit sums:

```text
10 → 1 + 0 = 1
12 → 1 + 2 = 3
13 → 1 + 3 = 4
14 → 1 + 4 = 5
```

New array:

```text
[1,3,4,5]
```

Minimum element:

```text
1
```

Output

```text
1
```

---

### Example 2

Input

```text
nums = [1,2,3,4]
```

Explanation

Digit sums:

```text
1 → 1
2 → 2
3 → 3
4 → 4
```

New array:

```text
[1,2,3,4]
```

Minimum element:

```text
1
```

Output

```text
1
```

---

### Example 3

Input

```text
nums = [999,19,29]
```

Explanation

Digit sums:

```text
999 → 9 + 9 + 9 = 27
19  → 1 + 9 = 10
29  → 2 + 9 = 11
```

New array:

```text
[27,10,11]
```

Minimum element:

```text
10
```

Output

```text
10
```

## Approach

Digit Sum Computation + Linear Minimum Search

## Intuition

For each number:

* Extract its digits one by one using `% 10`
* Add them to obtain the digit sum
* Track the smallest digit sum encountered

Since every element must be processed exactly once, a single traversal is sufficient.

## Algorithm Steps

* Initialize `mini` with a large value.
* Traverse every element in `nums`.
* For each number:

  * Compute its digit sum.
  * Compare the digit sum with `mini`.
  * Update `mini` if a smaller value is found.
* Return `mini`.

## Visual Walkthrough

### Case 1

```text
nums = [10,12,13,14]
```

Digit sums:

```text
10 → 1
12 → 3
13 → 4
14 → 5
```

Current minimum progression:

```text
∞ → 1 → 1 → 1 → 1
```

Answer:

```text
1
```

---

### Case 2

```text
nums = [999,19,29]
```

Digit sums:

```text
999 → 27
19  → 10
29  → 11
```

Minimum progression:

```text
∞ → 27 → 10 → 10
```

Answer:

```text
10
```

---

### Case 3

```text
nums = [5,50,500]
```

Digit sums:

```text
5   → 5
50  → 5
500 → 5
```

Minimum:

```text
5
```

Answer:

```text
5
```

## Complexity Analysis

### Time Complexity

**O(n × d)**

Where:

* `n` = number of elements
* `d` = number of digits in each number

For each element, we process all of its digits once.

Since `nums[i] ≤ 10^4`, `d` is at most 5, making this effectively **O(n)**.

### Space Complexity

**O(1)**

Only a few variables are used regardless of input size.

## Solution Explanation

The solution iterates through the array and computes the digit sum of every number by repeatedly extracting the last digit using modulo (`% 10`) and removing it using division (`/ 10`). After calculating the digit sum, it updates the minimum value found so far. Finally, the smallest digit sum is returned.

## Full Solution

### C++ Implementation

```cpp
#include <vector>
using namespace std;

class Solution {
public:
    int minElement(vector<int>& nums) {

        // Store array size
        int n = nums.size();

        // Variable to track minimum digit sum
        int mini = 10000;

        // Process every number in the array
        for(int i = 0; i < n; i++) {

            // Compute digit sum of current number
            int sum = 0;

            while(nums[i]) {

                // Add last digit
                sum += nums[i] % 10;

                // Remove last digit
                nums[i] /= 10;
            }

            // Update minimum digit sum
            if(sum < mini) {
                mini = sum;
            }
        }

        // Return the minimum digit sum found
        return mini;
    }
};
```

## Test Cases Analysis

| Input Array   | Digit Sums | Minimum |
| ------------- | ---------- | ------- |
| [10,12,13,14] | [1,3,4,5]  | 1       |
| [1,2,3,4]     | [1,2,3,4]  | 1       |
| [999,19,29]   | [27,10,11] | 10      |
| [5,50,500]    | [5,5,5]    | 5       |
| [10000]       | [1]        | 1       |

## Edge Cases to Consider

* Array with a single element
* Numbers containing many zeros
* All digit sums being equal
* Largest allowed value (`10000`)
* Minimum allowed value (`1`)

## Common Test Cases

* Mixed digit lengths
* Numbers with trailing zeros
* Repeated values
* Large digit sums (e.g., 9999)

## Common Mistakes to Avoid

* Forgetting to reset `sum` for each number
* Using the original number after modifying it during digit extraction
* Not updating the minimum after computing each digit sum

## Interview Relevance

* Tests digit manipulation fundamentals
* Evaluates basic array traversal skills
* Common warm-up problem involving number processing

## What This Problem Teaches

* Extracting digits using modulo and division
* Tracking aggregate values during traversal
* Efficient single-pass processing

## Key Takeaways

* Digit-sum computation is a common technique in coding interviews.
* A single traversal is enough to solve the problem efficiently.
* Maintaining a running minimum avoids extra storage.

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The challenge is straightforward: compute the digit sum of each element and track the smallest result. It primarily tests basic number manipulation and iteration skills.