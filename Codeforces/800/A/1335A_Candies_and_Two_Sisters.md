# A_Candies_and_Two_Sisters

## Platform

Codeforces

## Problem Link

[A. Candies and Two Sisters](https://codeforces.com/problemset/problem/1335/A)

## Problem Statement

Two sisters have `n` candies in total. They want to divide the candies between themselves such that:
* Each sister gets a **positive number** of candies (at least 1 candy each)
* One sister gets **strictly more** candies than the other (no equal distribution)

Your task is to find the **maximum number of ways** to distribute the candies satisfying these conditions.

## Input Format

* The first line contains an integer `t` - the number of test cases
* Each of the next `t` lines contains a single integer `n` - the total number of candies

## Output Format

For each test case, print a single integer representing the maximum number of ways to distribute the candies.

## Constraints

* `1 ≤ t ≤ 10^4`
* `2 ≤ n ≤ 10^9`

## Examples

### Example 1

**Input**
```
7
2
3
4
5
6
7
1000000000
```

**Explanation**

* **n = 2**: Only valid distribution is (1, 1), but this violates the "strictly more" condition → **0 ways**
* **n = 3**: Valid distribution is (1, 2) or (2, 1) → but they're the same unordered pair → **1 way**
* **n = 4**: Valid distributions are (1, 3) → **1 way** (since (3, 1) is the same unordered pair)
* **n = 5**: Valid distributions are (1, 4) and (2, 3) → **2 ways**
* **n = 6**: Valid distributions are (1, 5) and (2, 4) → **2 ways**
* **n = 7**: Valid distributions are (1, 6), (2, 5), (3, 4) → **3 ways**
* **n = 1000000000**: ⌊1000000000/2⌋ - 1 = **499999999 ways**

**Output**
```
0
1
1
2
2
3
499999999
```

### Example 2

**Input**
```
3
8
9
10
```

**Explanation**

* **n = 8**: Valid pairs are (1, 7), (2, 6), (3, 5) → **3 ways** (note: (4, 4) is invalid as it's equal)
* **n = 9**: Valid pairs are (1, 8), (2, 7), (3, 6), (4, 5) → **4 ways**
* **n = 10**: Valid pairs are (1, 9), (2, 8), (3, 7), (4, 6) → **4 ways** (note: (5, 5) is invalid)

**Output**
```
3
4
4
```

### Example 3

**Input**
```
2
2
100
```

**Explanation**

* **n = 2**: Cannot distribute 2 candies with one sister having strictly more → **0 ways**
* **n = 100**: Valid pairs from (1, 99) to (49, 51) → **49 ways**

**Output**
```
0
49
```

## Approach

Mathematical formula derivation based on parity (odd/even analysis).

## Intuition

The key insight is that we need to count unordered pairs (a, b) where:
* a + b = n
* a > 0 and b > 0
* a ≠ b (strictly different amounts)

Since we're counting unordered pairs and want a ≠ b, we only count pairs where a < b (to avoid double counting).

The valid range is: 1 ≤ a < n/2

**For odd n**: 
* We can have pairs (1, n-1), (2, n-2), ..., up to (⌊n/2⌋, ⌈n/2⌉)
* Total ways = ⌊n/2⌋ = n/2 (integer division)

**For even n**:
* We can have pairs (1, n-1), (2, n-2), ..., but NOT (n/2, n/2) as it violates a ≠ b
* Total ways = n/2 - 1

## Algorithm Steps

1. Read the number of test cases `t`
2. For each test case:
   * Read the number of candies `n`
   * Check if `n` is odd or even using bitwise AND operation (`n & 1`)
   * If `n` is odd:
     * Calculate result as `n / 2` (integer division)
   * If `n` is even:
     * Calculate result as `n / 2 - 1`
   * Print the result
3. Repeat for all test cases

## Visual Walkthrough

### Test Case 1: n = 7 (odd)

**All possible pairs:**
```
Sister 1  |  Sister 2  |  Valid?
    1          6           ✓ (different)
    2          5           ✓ (different)
    3          4           ✓ (different)
    4          3           (duplicate of (3,4))
    5          2           (duplicate of (2,5))
    6          1           (duplicate of (1,6))
```

**Unique valid distributions:** 3

**Formula:** ⌊7/2⌋ = 3 ✓

### Test Case 2: n = 8 (even)

**All possible pairs:**
```
Sister 1  |  Sister 2  |  Valid?
    1          7           ✓ (different)
    2          6           ✓ (different)
    3          5           ✓ (different)
    4          4           ✗ (equal - not allowed!)
    5          3           (duplicate of (3,5))
    6          2           (duplicate of (2,6))
    7          1           (duplicate of (1,7))
```

**Unique valid distributions:** 3

**Formula:** 8/2 - 1 = 4 - 1 = 3 ✓

### Test Case 3: n = 2 (even, edge case)

**All possible pairs:**
```
Sister 1  |  Sister 2  |  Valid?
    1          1           ✗ (equal - not allowed!)
```

**Unique valid distributions:** 0

**Formula:** 2/2 - 1 = 1 - 1 = 0 ✓

## Complexity Analysis

### Time Complexity

**O(t)**

* We process `t` test cases
* For each test case:
  * Reading input: O(1)
  * Checking parity (bitwise AND): O(1)
  * Integer division: O(1)
  * Output: O(1)
* Total: O(t × 1) = **O(t)**

### Space Complexity

**O(1)**

* We only use a constant number of variables (`t`, `n`, loop counter)
* No data structures that scale with input size
* Total auxiliary space: **O(1)**

## Solution Explanation

The solution leverages a mathematical pattern rather than brute force enumeration:

1. **Parity Check**: Uses bitwise AND (`n & 1`) to efficiently determine if n is odd
   * `n & 1 = 1` means n is odd
   * `n & 1 = 0` means n is even

2. **Formula Application**:
   * **Odd n**: The middle pair will always have different values (e.g., for n=7: (3,4)), so we count all pairs up to the middle: ⌊n/2⌋
   * **Even n**: The middle pair would be equal (e.g., for n=8: (4,4)), which is invalid, so we exclude it: n/2 - 1

3. **Efficiency**: Instead of iterating through all pairs, we use direct mathematical calculation, making it work even for n up to 10^9

This approach is elegant, efficient, and demonstrates the power of mathematical insight in competitive programming.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {
    // Read number of test cases
    int t;
    cin >> t;
    
    // Process each test case
    while(t--) {
        // Read total number of candies
        int n;
        cin >> n;
        
        // Check if n is odd or even using bitwise AND
        // n & 1 returns 1 if n is odd, 0 if n is even
        if(n & 1) {
            // If n is odd:
            // Number of ways = floor(n/2)
            // Example: n=7 → 7/2 = 3 ways: (1,6), (2,5), (3,4)
            n = n / 2;
        } else {
            // If n is even:
            // Number of ways = n/2 - 1
            // We subtract 1 to exclude the equal distribution
            // Example: n=8 → 8/2 - 1 = 3 ways: (1,7), (2,6), (3,5)
            // We exclude (4,4) as it violates the "strictly more" condition
            n = n / 2 - 1;
        }
        
        // Output the result for this test case
        cout << n << endl;
    }
    
    return 0;
}
```

## Test Cases Analysis

| n | Parity | Middle Pair | Formula Applied | Expected Output |
|---|--------|-------------|-----------------|-----------------|
| 2 | Even | (1, 1) invalid | 2/2 - 1 | 0 |
| 3 | Odd | (1, 2) valid | 3/2 | 1 |
| 7 | Odd | (3, 4) valid | 7/2 | 3 |
| 8 | Even | (4, 4) invalid | 8/2 - 1 | 3 |
| 100 | Even | (50, 50) invalid | 100/2 - 1 | 49 |
| 1000000000 | Even | Large | 10^9/2 - 1 | 499999999 |

## Edge Cases to Consider

* **Minimum valid input**: n = 2 (should return 0)
* **Small odd number**: n = 3 (should return 1)
* **Small even number**: n = 4 (should return 1)
* **Large even number**: n = 10^9 (tests integer overflow handling)
* **Large odd number**: n = 999999999 (tests large number calculations)
* **Maximum test cases**: t = 10^4 with varying n values

## Common Test Cases

* Powers of 2 (2, 4, 8, 16, 32, ...)
* Consecutive numbers to verify pattern
* Very large numbers close to constraint limit
* Mix of odd and even numbers in multiple test cases

## Common Mistakes to Avoid

* **Using floating-point division** instead of integer division - can lead to precision errors
* **Forgetting to subtract 1 for even numbers** - would incorrectly count the equal distribution
* **Not handling the n=2 edge case** properly - should return 0, not negative value
* **Integer overflow** when dealing with n close to 10^9 (though this problem's formula doesn't cause overflow)

## Interview Relevance

* Tests **pattern recognition** and ability to derive mathematical formulas
* Evaluates **optimization thinking** - avoiding brute force when a formula exists
* Assesses understanding of **parity checks** and efficient conditionals
* Demonstrates **problem simplification** skills

## What This Problem Teaches

* Looking for mathematical patterns instead of iterating through all possibilities
* Understanding the relationship between problem constraints and solution complexity
* Using bitwise operations for efficient parity checking
* Recognizing when brute force is unnecessary

## Key Takeaways

* **Mathematical insight** can reduce O(n) problems to O(1)
* **Parity matters** - odd and even cases often require different handling
* **Bitwise operations** (`n & 1`) are faster than modulo for parity checks
* **Edge cases** like n=2 require special attention in formula derivation
* **Large constraints** (n up to 10^9) hint that iteration-based solutions won't work

## Problem Difficulty Analysis

This is an **Easy-level** problem, but with a mathematical twist. It focuses on:
* Pattern recognition and formula derivation
* Basic arithmetic and parity analysis
* Efficient conditional logic
* Understanding constraints to guide solution approach

The problem is excellent for teaching beginners that not every problem requires loops or complex algorithms - sometimes pure mathematics is the most elegant solution. It's commonly used in contests to test mathematical thinking and optimization awareness.