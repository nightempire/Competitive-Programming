# A_Is_your_horseshoe_on_the_other_hoof

## Platform

Codeforces

## Problem Link

[A. Is your horseshoe on the other hoof?](https://codeforces.com/problemset/problem/228/A)

## Problem Statement

Valera has decided to go jogging in new sneakers. Before going outside, he must wear **four horseshoes**, one on each hoof.

Valera owns four horseshoes, each possibly of a different color.
To look stylish, **all four horseshoes must be of different colors**.

If some horseshoes have the same color, Valera needs to buy additional horseshoes so that all four colors are distinct.

Your task is to determine **how many new horseshoes Valera must buy**.

## Input Format

* A single line containing **four integers**
  `a, b, c, d`

Each integer represents the color of one horseshoe.

## Output Format

* Print a single integer
  The minimum number of horseshoes Valera needs to buy.

## Constraints

* Exactly 4 integers are given
* `1 ≤ a, b, c, d ≤ 10^9`
* Colors are represented as integers

## Examples

### Example 1

Input

```
1 7 3 3
```

Explanation

* Colors `3` and `3` are the same
* Only 3 distinct colors exist
* Valera must buy **1** new horseshoe

Output

```
1
```

---

### Example 2

Input

```
1 2 3 4
```

Explanation

* All four colors are already distinct
* No additional horseshoes are required

Output

```
0
```

---

### Example 3

Input

```
5 5 5 5
```

Explanation

* All horseshoes have the same color
* Only 1 distinct color exists
* Valera must buy **3** new horseshoes

Output

```
3
```

## Approach

**Duplicate elimination using conditional comparison and counting**

## Intuition

The core requirement is to identify **how many colors are repeated** among the four horseshoes.

Instead of explicitly counting unique elements using data structures, the given solution progressively **invalidates duplicate values** by setting them to zero.

After removing duplicates, the number of zero-valued entries directly indicates how many horseshoes need replacement.

## Algorithm Steps

* Read four integers representing horseshoe colors
* Compare the second color with the first
  If equal, invalidate it
* Compare the third color with the first two
  If equal to any, invalidate it
* Compare the fourth color with the first three
  If equal to any, invalidate it
* Count how many values are invalidated
* Output that count

## Visual Walkthrough

### Case 1

Input

```
1 7 3 3
```

Processing

```
a = 1
b = 7
c = 3
d = 3 → duplicate of c → invalidated
```

Invalid values count = 1
Result = 1

---

### Case 2

Input

```
2 2 3 3
```

Processing

```
b duplicates a → invalidated
d duplicates c → invalidated
```

Invalid values count = 2
Result = 2

---

### Case 3

Input

```
4 4 4 4
```

Processing

```
b duplicates a → invalidated
c duplicates a → invalidated
d duplicates a → invalidated
```

Invalid values count = 3
Result = 3

## Complexity Analysis

### Time Complexity

**O(1)**

Only a fixed number of comparisons are performed regardless of input values.

### Space Complexity

**O(1)**

No additional data structures are used. Only four integer variables are maintained.

## Solution Explanation

The solution works by **eliminating duplicate colors step by step**.
Each time a duplicate is found, that variable is set to zero.

Finally, the logical NOT operator (`!`) is used to count how many values became zero.
This count directly corresponds to the number of horseshoes that must be replaced.

The approach is compact, efficient, and well-suited for fixed-size input problems.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Four integers representing the colors of the horseshoes
    int a, b, c, d;
    cin >> a >> b >> c >> d;

    // If the second horseshoe has the same color as the first,
    // invalidate it by setting it to zero
    if (a == b)
        b = 0;

    // If the third horseshoe matches either the first or second,
    // invalidate it
    if (a == c || b == c)
        c = 0;

    // If the fourth horseshoe matches any of the previous ones,
    // invalidate it
    if (a == d || b == d || c == d)
        d = 0;

    // Count how many horseshoes were invalidated
    // !x evaluates to 1 if x == 0, otherwise 0
    cout << !a + !b + !c + !d << endl;

    return 0;
}
```

## Test Cases Analysis

| Input   | Distinct Colors | Horseshoes to Buy |
| ------- | --------------- | ----------------- |
| 1 2 3 4 | 4               | 0                 |
| 1 7 3 3 | 3               | 1                 |
| 5 5 5 5 | 1               | 3                 |
| 2 2 3 4 | 3               | 1                 |

## Edge Cases to Consider

* All four colors are identical
* Exactly two colors are duplicated
* Colors have very large integer values

## Common Test Cases

* Already distinct horseshoes
* One duplicate pair
* Multiple duplicates

## Common Mistakes to Avoid

* Forgetting that only **four inputs** exist
* Overcomplicating with unnecessary data structures
* Miscounting duplicates instead of missing colors

## Interview Relevance

* Tests understanding of duplicates and uniqueness
* Encourages optimized thinking for small input sizes
* Demonstrates alternative logic without using sets or maps

## What This Problem Teaches

* Handling fixed-size input efficiently
* Logical elimination techniques
* Creative use of boolean evaluation in counting

## Key Takeaways

* Simpler inputs allow simpler solutions
* Not every problem requires advanced data structures
* Clear logic improves both performance and readability

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on logical reasoning and careful comparison rather than algorithmic complexity, making it ideal for beginners and competitive programming warm-ups.