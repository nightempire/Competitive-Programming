## 2144. Minimum Cost of Buying Candies With Discount

## Platform

LeetCode

## Problem Link

[Minimum Cost of Buying Candies With Discount](https://leetcode.com/problems/minimum-cost-of-buying-candies-with-discount/)

## Problem Statement

A shop is selling candies. You are given an integer array `cost` where `cost[i]` is the price of the `iᵗʰ` candy.

The shop offers the following discount:

* For every purchase of **three candies**, you pay for the **two most expensive candies** and get the **least expensive candy for free**.

Your task is to determine the **minimum total cost** required to buy all the candies.

## Input Format

* An integer array `cost`

## Output Format

* Return an integer representing the minimum amount of money needed to buy all candies.

## Constraints

* `1 ≤ cost.length ≤ 100`
* `1 ≤ cost[i] ≤ 100`

## Examples

### Example 1

Input

```text
cost = [1,2,3]
```

Explanation

Sort in descending order:

```text
[3,2,1]
```

Buy three candies together:

```text
Pay: 3 + 2
Free: 1
```

Total cost:

```text
5
```

Output

```text
5
```

---

### Example 2

Input

```text
cost = [6,5,7,9,2,2]
```

Explanation

Sort descending:

```text
[9,7,6,5,2,2]
```

Group into threes:

```text
(9,7,6) → pay 9 + 7, free 6
(5,2,2) → pay 5 + 2, free 2
```

Total:

```text
9 + 7 + 5 + 2 = 23
```

Output

```text
23
```

---

### Example 3

Input

```text
cost = [5,5]
```

Explanation

Only two candies exist.

```text
Pay: 5 + 5
```

No discount applies.

Output

```text
10
```

## Approach

Greedy Sorting

## Intuition

To maximize the discount, the free candy should be as expensive as possible.

After sorting the candies in **descending order**:

* Every group of three candies becomes:

```text
Most Expensive
Second Most Expensive
Third Most Expensive
```

The third candy in each group is automatically the cheapest among those three and can be taken for free.

Thus:

* Add the cost of the first two candies.
* Skip every third candy.

## Algorithm Steps

* Sort the array in descending order.
* Initialize `ans = 0`.
* Traverse the sorted array.
* For every group of three candies:

  * Add the first candy.
  * Add the second candy.
  * Skip the third candy.
* Return the accumulated cost.

## Visual Walkthrough

### Case 1

```text
cost = [1,2,3]
```

After sorting:

```text
[3,2,1]
```

Processing:

```text
3 → Pay
2 → Pay
1 → Free
```

Total:

```text
5
```

---

### Case 2

```text
cost = [6,5,7,9,2,2]
```

After sorting:

```text
[9,7,6,5,2,2]
```

Processing:

```text
9 → Pay
7 → Pay
6 → Free

5 → Pay
2 → Pay
2 → Free
```

Total:

```text
23
```

---

### Case 3

```text
cost = [8,4,3,2]
```

After sorting:

```text
[8,4,3,2]
```

Processing:

```text
8 → Pay
4 → Pay
3 → Free
2 → Pay
```

Total:

```text
14
```

## Complexity Analysis

### Time Complexity

**O(n log n)**

Sorting dominates the running time.

```text
Sorting: O(n log n)
Traversal: O(n)
```

Overall:

```text
O(n log n)
```

### Space Complexity

**O(1)**

The sorting is performed in-place (ignoring sorting implementation space).

## Solution Explanation

The solution first sorts all candy prices in descending order.

After sorting, every third candy represents the cheapest candy in its group of three. Since the discount allows this candy to be obtained for free, the algorithm simply skips adding its cost to the answer.

The variable `i` is used to track positions:

```text
Position 1 → Pay
Position 2 → Pay
Position 3 → Free

Position 4 → Pay
Position 5 → Pay
Position 6 → Free
...
```

This ensures the maximum possible discount while purchasing all candies.

## Full Solution

### C++ Implementation

```cpp
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    int minimumCost(vector<int>& cost) {

        // Sort candies in descending order
        // so that every third candy in a group
        // becomes the free candy
        sort(cost.begin(), cost.end(), greater<int>());

        // Stores the final minimum cost
        int ans = 0;

        // Position counter (1-based indexing)
        int i = 1;

        // Traverse all candies
        for(int &c : cost) {

            // Add the cost of first and second
            // candy in every group of three
            if(i % 3) {
                ans += c;
            }

            // Move to next position
            i++;
        }

        // Return minimum total cost
        return ans;
    }
};
```

## Test Cases Analysis

| Cost Array     | Sorted Array   | Free Candies | Total Cost |
| -------------- | -------------- | ------------ | ---------- |
| [1,2,3]        | [3,2,1]        | 1            | 5          |
| [6,5,7,9,2,2]  | [9,7,6,5,2,2]  | 6,2          | 23         |
| [5,5]          | [5,5]          | None         | 10         |
| [8,4,3,2]      | [8,4,3,2]      | 3            | 14         |
| [10,9,8,7,6,5] | [10,9,8,7,6,5] | 8,5          | 32         |

## Edge Cases to Consider

* Only one candy.
* Only two candies.
* Exactly three candies.
* All candies have the same cost.
* Maximum allowed number of candies.

## Common Test Cases

* Array length divisible by 3.
* Array length not divisible by 3.
* Strictly increasing costs.
* Strictly decreasing costs.
* Repeated candy prices.

## Common Mistakes to Avoid

* Sorting in ascending order instead of descending order.
* Forgetting to skip every third candy.
* Trying to form groups before sorting.

## Interview Relevance

* Classic greedy optimization problem.
* Tests sorting-based decision making.
* Demonstrates maximizing discounts through ordering.

## What This Problem Teaches

* Greedy strategy design.
* Using sorting to maximize benefits.
* Grouping elements efficiently.

## Key Takeaways

* To maximize the discount, make the free candy as expensive as possible.
* Sorting in descending order naturally creates optimal groups.
* Every third candy after sorting becomes free.

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The primary challenge is recognizing the greedy observation that sorting the candies in descending order maximizes the value of the free candies. Once this insight is identified, the implementation is straightforward.