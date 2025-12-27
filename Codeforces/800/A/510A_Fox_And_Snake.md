# A_Fox_And_Snake

## Platform

Codeforces

## Problem Link

[A. Fox And Snake](https://codeforces.com/problemset/problem/510/A)

## Problem Statement

Fox Ciel wants to draw a snake pattern consisting of `n` rows and `m` columns using hash symbols (`#`) and dots (`.`).

The snake pattern follows these rules:
* All **odd-numbered rows** (1st, 3rd, 5th, etc.) are completely filled with hash symbols
* **Even-numbered rows** alternate between having a hash symbol on the **rightmost** position or the **leftmost** position
* The first even row has a hash on the right, the second even row has a hash on the left, and this pattern continues alternating

Your task is to print the snake pattern for given dimensions `n` × `m`.

## Input Format

* A single line containing two integers `n` and `m`:
  * `n` - the number of rows
  * `m` - the number of columns

## Output Format

Print `n` lines, each containing `m` characters, representing the snake pattern.

## Constraints

* `3 ≤ n, m ≤ 50`
* `n` is **odd**

## Examples

### Example 1

**Input**
```
3 3
```

**Explanation**
* Row 1 (odd): All hash symbols → `###`
* Row 2 (even, first): Hash on the right → `..#`
* Row 3 (odd): All hash symbols → `###`

**Output**
```
###
..#
###
```

### Example 2

**Input**
```
3 4
```

**Explanation**
* Row 1 (odd): All hash symbols → `####`
* Row 2 (even, first): Hash on the right → `...#`
* Row 3 (odd): All hash symbols → `####`

**Output**
```
####
...#
####
```

### Example 3

**Input**
```
5 3
```

**Explanation**
* Row 1 (odd): All hash symbols → `###`
* Row 2 (even, first): Hash on the right → `..#`
* Row 3 (odd): All hash symbols → `###`
* Row 4 (even, second): Hash on the left → `#..`
* Row 5 (odd): All hash symbols → `###`

**Output**
```
###
..#
###
#..
###
```

## Approach

Pattern generation with conditional alternation.

## Intuition

The problem requires generating a specific visual pattern. We can break it down into two components:
1. **Odd rows** always have the same pattern (all hash symbols)
2. **Even rows** alternate between having a hash on the right side and left side

By tracking which even row we're on using a boolean flag, we can alternate the position of the hash symbol efficiently.

## Algorithm Steps

1. Read input values `n` (rows) and `m` (columns)
2. Create two string templates:
   * `s1`: A string of `m` hash symbols (for odd rows)
   * `s2`: A string of `m-1` dots (for even rows base)
3. Print the first row (which is always `s1`)
4. Initialize a boolean flag to track even row alternation
5. Loop through remaining rows (starting from row 2):
   * For even rows:
     * If flag is true: place hash at rightmost position
     * If flag is false: place hash at leftmost position
     * Toggle the flag for next even row
   * For odd rows: print `s1` (all hash symbols)
6. Continue until all `n` rows are printed

## Visual Walkthrough

### Test Case 1: n=5, m=4

**Step 1**: Create base strings
```
s1 = "####"  (all hash symbols)
s2 = "..."   (all dots, will modify one position)
```

**Step 2**: Print first row (odd)
```
Output: ####
```

**Step 3**: Process row 2 (even, flag=true)
```
s2[3] = '#'  → "...#"
Output: ...#
flag = false
```

**Step 4**: Print row 3 (odd)
```
Output: ####
```

**Step 5**: Process row 4 (even, flag=false)
```
s2[0] = '#'  → "#..."
Output: #...
flag = true
```

**Step 6**: Print row 5 (odd)
```
Output: ####
```

**Final Output:**
```
####
...#
####
#...
####
```

### Test Case 2: n=3, m=3

**Rows:**
```
Row 1 (odd):  ###
Row 2 (even): ..#  (first even row → right)
Row 3 (odd):  ###
```

**Final Output:**
```
###
..#
###
```

## Complexity Analysis

### Time Complexity

**O(n × m)**

* Building `s1` and `s2` strings takes O(m) time
* Printing each row takes O(m) time
* We print `n` rows in total
* Total: O(m) + O(n × m) = **O(n × m)**

### Space Complexity

**O(m)**

* We store two strings `s1` and `s2`, each of length `m`
* No additional data structures that scale with input
* Total auxiliary space: **O(m)**

## Solution Explanation

The solution efficiently generates the snake pattern by:
1. Pre-building template strings for odd rows (all hashes) and even rows (mostly dots)
2. Using a boolean flag to alternate the hash position in even rows
3. Modifying only one character position in the even row template before printing

This approach avoids rebuilding strings from scratch for each row, making it both time and space efficient. The alternating flag elegantly handles the zigzag pattern of the snake's tail.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {
    // Read the dimensions of the snake pattern
    int n, m;
    cin >> n >> m;
    
    // Create template strings:
    // s1 - for odd rows (all hash symbols)
    // s2 - for even rows (base with dots)
    string s1 = "#", s2 = ".";
    
    // Build s1 with m hash symbols
    // Build s2 with m dots
    for(int i = 1; i < m; i++) {
        s1 += "#";
        s2 += ".";
    }
    
    // Print the first row (always all hashes)
    cout << s1 << endl;
    
    // Flag to track which side the hash should be on
    // true = right side, false = left side
    bool flag = 1;
    
    // Process remaining rows starting from row 2
    // Increment by 2 since we process both even and odd rows in each iteration
    for(int i = 1; i < n; i += 2) {
        
        // Handle even row
        if(flag) {
            // Place hash on the rightmost position
            s2[m - 1] = '#';
            cout << s2 << endl;
            // Reset it back to dot for next use
            s2[m - 1] = '.';
        } else {
            // Place hash on the leftmost position
            s2[0] = '#';
            cout << s2 << endl;
            // Reset it back to dot for next use
            s2[0] = '.';
        }
        
        // Toggle flag for next even row
        flag = !flag;
        
        // Print the next odd row (all hashes)
        cout << s1 << endl;
    }
    
    return 0;
}
```

## Test Cases Analysis

| Input (n, m) | Pattern Type | Hash Positions in Even Rows | Expected Lines |
|--------------|--------------|----------------------------|----------------|
| (3, 3) | Minimal | Right only | 3 |
| (5, 3) | Small | Right, Left | 5 |
| (3, 4) | Wide | Right only | 3 |
| (7, 5) | Medium | Right, Left, Right | 7 |
| (50, 50) | Maximum | Alternating 25 times | 50 |

## Edge Cases to Consider

* **Minimum dimensions**: n=3, m=3 (smallest valid input)
* **Wide snake**: Large m with small n (e.g., n=3, m=50)
* **Tall snake**: Large n with small m (e.g., n=49, m=3)
* **Maximum dimensions**: n=50, m=50 (stress test)
* **Single even row**: n=3 (only one even row to print)

## Common Test Cases

* Standard square grids (n=m)
* Rectangular grids where n ≠ m
* Cases with multiple even rows to verify alternation
* Boundary cases at constraint limits

## Common Mistakes to Avoid

* **Off-by-one errors** in string indexing - remember rightmost position is `m-1`, not `m`
* **Forgetting to reset** the modified character in `s2` back to dot after printing
* **Incorrect loop increment** - must increment by 2 since we handle both even and odd rows in each iteration

## Interview Relevance

* Tests **pattern recognition** and ability to identify repetitive structures
* Evaluates **string manipulation** skills in chosen programming language
* Assesses understanding of **boolean flags** for alternating behavior

## What This Problem Teaches

* Breaking down visual patterns into logical rules
* Efficient string template reuse to avoid redundant construction
* Using boolean flags for alternating states
* Importance of resetting state when reusing templates

## Key Takeaways

* **Template reuse** is more efficient than rebuilding strings from scratch
* **Visual patterns** can often be decomposed into simpler alternating rules
* **Boolean flags** are elegant solutions for two-state alternation
* **Character-by-character modification** is useful for pattern variations

## Problem Difficulty Analysis

This is an **Easy-level** problem suitable for beginners. It focuses on:
* Basic input/output operations
* String manipulation fundamentals
* Simple conditional logic
* Loop control and iteration

The problem serves as an excellent introduction to pattern generation problems and is commonly used as a warm-up in programming contests.