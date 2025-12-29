# A_Soft_Drinking

## Platform

Codeforces

## Problem Link

[A. Soft Drinking](https://codeforces.com/problemset/problem/151/A)

## Problem Statement

A group of `n` friends plans to drink soft drinks together. They have several resources available:

* `k` bottles of soft drink, each containing `l` milliliters
* `c` limes, each cut into `d` slices
* `p` grams of salt

Each friend needs:

* `nl` milliliters of drink
* `np` grams of salt

A friend can drink only if **all three components** (drink, lime slice, and salt) are available.

Determine the **maximum number of toasts** each friend can make.

## Input Format

A single line containing eight integers:

```
n k l c d p nl np
```

## Output Format

Print a single integer representing the number of toasts **each friend** can make.

## Constraints

* `1 ≤ n ≤ 1000`
* `1 ≤ k, l, c, d, p, nl, np ≤ 1000`

## Examples

### Example 1

Input

```
3 4 5 10 8 100 3 1
```

Explanation

* Total drink = `4 × 5 = 20 ml` → `20 / 3 = 6` toasts
* Total lime slices = `10 × 8 = 80` slices
* Total salt = `100 / 1 = 100` toasts possible

Minimum = `6`
Per friend = `6 / 3 = 2`

Output

```
2
```

### Example 2

Input

```
5 100 10 1 19 90 4 3
```

Explanation

* Drink toasts = `(100 × 10) / 4 = 250`
* Lime toasts = `1 × 19 = 19`
* Salt toasts = `90 / 3 = 30`

Minimum = `19`
Per friend = `19 / 5 = 3`

Output

```
3
```

### Example 3

Input

```
1 1 1 1 1 1 1 1
```

Explanation

All resources allow exactly one toast.

Output

```
1
```

## Approach

**Resource Limitation Analysis (Greedy Minimum Selection)**

## Intuition

Each toast requires all three resources simultaneously.
The limiting factor is the resource that runs out first.

So:

* Compute how many toasts each resource can support
* Take the minimum of those values
* Divide by the number of friends

## Algorithm Steps

* Read all input values
* Compute total drink available and convert to possible toasts
* Compute total lime slices available
* Compute total salt-based toasts
* Find the minimum among all three
* Divide by number of friends
* Output the result

## Visual Walkthrough

Consider this input:

```
n = 3, k = 4, l = 5, c = 10, d = 8, p = 100, nl = 3, np = 1
```

Drink calculation:

```
Total drink = 4 × 5 = 20 ml
Toasts from drink = 20 / 3 = 6
```

Lime calculation:

```
Total lime slices = 10 × 8 = 80
```

Salt calculation:

```
Toasts from salt = 100 / 1 = 100
```

Final decision:

```
Minimum = 6
Each friend = 6 / 3 = 2
```

## Complexity Analysis

### Time Complexity

O(1)

All calculations are constant-time arithmetic operations.

### Space Complexity

O(1)

Only a fixed number of integer variables are used.

## Solution Explanation

The solution computes the number of possible toasts based on each available resource independently. Since every toast requires all three resources, the minimum number of supported toasts determines the final answer. Dividing this value by the number of friends gives the maximum number of toasts per friend.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // n  -> number of friends
    // k  -> number of bottles
    // l  -> milliliters per bottle
    // c  -> number of limes
    // d  -> slices per lime
    // p  -> grams of salt
    // nl -> milliliters needed per toast
    // np -> grams of salt needed per toast
    int n, k, l, c, d, p, nl, np;
    cin >> n >> k >> l >> c >> d >> p >> nl >> np;

    // Calculate how many toasts can be made from drink
    // Total drink = k * l
    // Each toast requires nl milliliters
    int x = (k * l) / nl;

    // Calculate how many toasts can be made from lime slices
    // Each lime has d slices
    int y = c * d;

    // Calculate how many toasts can be made from salt
    // Each toast requires np grams
    int z = p / np;

    // The limiting resource determines the total number of toasts
    // Divide by number of friends to get toasts per friend
    cout << min(x, min(y, z)) / n << '\n';

    return 0;
}
```

## Test Cases Analysis

| Drink Toasts | Lime Toasts | Salt Toasts | Friends | Output |
| ------------ | ----------- | ----------- | ------- | ------ |
| 6            | 80          | 100         | 3       | 2      |
| 250          | 19          | 30          | 5       | 3      |
| 1            | 1           | 1           | 1       | 1      |

## Edge Cases to Consider

* One resource is exactly sufficient while others are abundant
* Minimum values for all inputs
* Large values where division truncation matters

## Common Test Cases

* Drink is the limiting factor
* Lime slices are the limiting factor
* Salt is the limiting factor

## Common Mistakes to Avoid

* Forgetting integer division behavior
* Dividing before taking the minimum
* Missing one of the three constraints

## Interview Relevance

* Tests greedy decision-making
* Evaluates understanding of constraints
* Checks attention to integer arithmetic

## What This Problem Teaches

* Identifying bottleneck resources
* Translating real-world constraints into arithmetic logic
* Writing clean and efficient constant-time solutions

## Key Takeaways

* Always identify the limiting factor in multi-resource problems
* Greedy minimum selection is often sufficient
* Clear variable naming improves readability

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on arithmetic reasoning and constraint handling rather than complex algorithms, making it suitable for beginners and interview warm-up rounds.