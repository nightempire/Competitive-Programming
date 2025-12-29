# A_I_love_username

## Platform

Codeforces

## Problem Link

[A. I Love Username](https://codeforces.com/problemset/problem/155/A)

## Problem Statement

A user tracks their performance across multiple contests.  
For each contest, a score is recorded.

A score is considered **amazing** if it is **strictly greater than all previous scores** or **strictly smaller than all previous scores**.

The first score is not considered amazing.

Given the sequence of scores, determine how many amazing performances occurred.

## Input Format

- The first line contains an integer `n`, the number of contests.
- The second line contains `n` integers representing the scores in chronological order.

## Output Format

Print a single integer representing the number of amazing performances.

## Constraints

- `1 ≤ n ≤ 1000`
- `0 ≤ score ≤ 10000`

## Examples

### Example 1

Input
```
5
100 50 200 150 300
```

Explanation

- Contest 2: `50` is less than all previous → amazing
- Contest 3: `200` is greater than all previous → amazing
- Contest 4: `150` → not amazing
- Contest 5: `300` is greater than all previous → amazing

Output
```
3
```

### Example 2

Input
```
4
10 10 10 10
```

Explanation  
No score is strictly greater or strictly smaller than previous scores.

Output
```
0
```

### Example 3

Input
```
3
1 2 3
```

Explanation  
Each new score is greater than all previous.

Output
```
2
```

## Approach

**Single Pass Tracking of Extremes**

## Intuition

At any point, a score can only be amazing if it breaks a **previous maximum** or **previous minimum**.

By maintaining the current maximum and minimum while traversing the array, we can efficiently detect such cases in one pass.

## Algorithm Steps

- Read the number of contests
- Store all scores
- Initialize both minimum and maximum using the first score
- Traverse from the second score onward
- If the current score exceeds the maximum, update maximum and increment count
- If the current score is smaller than the minimum, update minimum and increment count
- Output the count

## Visual Walkthrough

Consider scores:
```
100 50 200 150 300
```

Initialization:
```
min = 100, max = 100
```

Step-by-step:
```
50   → new min → amazing
200  → new max → amazing
150  → no change
300  → new max → amazing
```

Total amazing performances:
```
3
```

Another case:
```
10 10 10 10
```

No strict changes → `0` amazing performances.

## Complexity Analysis

### Time Complexity

O(n)

Each score is processed exactly once.

### Space Complexity

O(n)

An array is used to store the scores.

## Solution Explanation

The solution keeps track of the highest and lowest scores seen so far.  
Whenever a new score exceeds either boundary, it qualifies as an amazing performance.  
This approach ensures efficiency and correctness using a single traversal.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of contests
    int n;
    cin >> n;

    // Array to store scores
    int nums[n];
    for (int i = 0; i < n; i++) {
        cin >> nums[i];
    }

    // Initialize minimum and maximum with the first score
    int max = nums[0];
    int min = nums[0];

    // Counter for amazing performances
    int count = 0;

    // Start checking from the second contest
    for (int i = 1; i < n; i++) {

        // If current score is a new maximum
        if (nums[i] > max) {
            max = nums[i];
            count++;
        }
        // If current score is a new minimum
        else if (nums[i] < min) {
            min = nums[i];
            count++;
        }
    }

    // Output the total number of amazing performances
    cout << count << '\n';

    return 0;
}
```

## Test Cases Analysis

| Scores Pattern            | n | Amazing Performances |
|--------------------------|---|---------------------|
| Increasing sequence      | 5 | 4                   |
| Decreasing sequence      | 5 | 4                   |
| Constant values          | 4 | 0                   |
| Mixed values             | 5 | Depends on extremes |

## Edge Cases to Consider

- Only one contest (`n = 1`)
- All scores equal
- Strictly increasing scores
- Strictly decreasing scores

## Common Test Cases

- First decrease then increase
- Alternating high and low values
- Large values within constraints

## Common Mistakes to Avoid

- Counting the first score as amazing
- Using non-strict comparisons (`>=` or `<=`)
- Forgetting to update min/max values

## Interview Relevance

- Tests array traversal logic
- Evaluates boundary tracking
- Common introductory greedy problem

## What This Problem Teaches

- Importance of maintaining running extremes
- Efficient single-pass algorithms
- Translating conditions into clean logic

## Key Takeaways

- Track only what matters: min and max
- Strict comparison is critical
- Simple logic can solve problems efficiently

## Problem Difficulty Analysis

This is an **Easy-level** problem.  
It emphasizes logical thinking and careful condition handling, making it ideal for beginners and coding interviews.