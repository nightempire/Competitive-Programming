# A_Games

## Platform

Codeforces

## Problem Link

[A. Games](https://codeforces.com/problemset/problem/268/A)

## Problem Statement

There are `n` football teams participating in a tournament. Each team has two uniforms: a **home uniform** and an **guest (away) uniform**, each with a specific color.

When two teams play against each other:
* The **home team** wears their **home uniform**
* The **guest team** wears their **guest uniform**

A game is considered to have a **uniform conflict** if the home team's home uniform color matches the guest team's guest uniform color.

Given the uniform colors for all teams, determine the total number of games where there will be a uniform conflict. Note that each pair of teams plays exactly twice (once with each team as the home team).

## Input Format

* The first line contains an integer `n` - the number of teams
* The next `n` lines each contain two integers `h` and `a`:
  * `h` - the color of the home uniform (represented as an integer)
  * `a` - the color of the guest uniform (represented as an integer)

## Output Format

Print a single integer representing the total number of games with uniform conflicts.

## Constraints

* `2 ≤ n ≤ 30`
* `1 ≤ h, a ≤ 100`

## Examples

### Example 1

**Input**
```
2
1 2
2 1
```

**Explanation**

Teams and their uniforms:
* Team 1: home = 1, guest = 2
* Team 2: home = 2, guest = 1

Games to check:
* Team 1 (home) vs Team 2 (guest): home uniform 1 vs guest uniform 1 → **Conflict!**
* Team 2 (home) vs Team 1 (guest): home uniform 2 vs guest uniform 2 → **Conflict!**

Total conflicts: 2

**Output**
```
2
```

### Example 2

**Input**
```
3
1 2
2 3
1 4
```

**Explanation**

Teams and their uniforms:
* Team 1: home = 1, guest = 2
* Team 2: home = 2, guest = 3
* Team 3: home = 1, guest = 4

Games to check:
* Team 1 vs Team 2 (guest): 1 ≠ 3 → No conflict
* Team 1 vs Team 3 (guest): 1 ≠ 4 → No conflict
* Team 2 vs Team 1 (guest): 2 = 2 → **Conflict!**
* Team 2 vs Team 3 (guest): 2 ≠ 4 → No conflict
* Team 3 vs Team 1 (guest): 1 ≠ 2 → No conflict
* Team 3 vs Team 2 (guest): 1 ≠ 3 → No conflict

Total conflicts: 1

**Output**
```
1
```

### Example 3

**Input**
```
4
100 42
42 100
5 5
100 3
```

**Explanation**

Teams and their uniforms:
* Team 1: home = 100, guest = 42
* Team 2: home = 42, guest = 100
* Team 3: home = 5, guest = 5
* Team 4: home = 100, guest = 3

Conflicts occur when:
* Team 1 (home) vs Team 2 (guest): 100 = 100 → **Conflict!**
* Team 2 (home) vs Team 1 (guest): 42 = 42 → **Conflict!**
* Team 4 (home) vs Team 2 (guest): 100 = 100 → **Conflict!**

Total conflicts: 3

**Output**
```
3
```

## Approach

Brute force comparison using nested loops.

## Intuition

The problem requires checking every possible game between teams. Since each team can be the home team against every other team, we need to check all ordered pairs of teams.

For each potential game, we compare:
* The **home team's home uniform color** with
* The **guest team's guest uniform color**

If these colors match, we increment our conflict counter. The nested loop naturally handles checking all possible games (n × n comparisons, including cases where i = j, though a team doesn't play against itself).

## Algorithm Steps

1. Read the number of teams `n`
2. Create a 2D array to store uniform colors for each team
   * `uniforms[i][0]` = home uniform color for team i
   * `uniforms[i][1]` = guest uniform color for team i
3. Read uniform colors for all `n` teams
4. Initialize a counter `count` to 0
5. Use nested loops to check all possible games:
   * Outer loop: iterate through each team as the home team (index `i`)
   * Inner loop: iterate through each team as the guest team (index `j`)
   * Compare `uniforms[i][0]` (home team's home uniform) with `uniforms[j][1]` (guest team's guest uniform)
   * If they match, increment `count`
6. Output the total count

## Visual Walkthrough

### Test Case 1: n=2

**Input:**
```
Team 1: home=1, guest=2
Team 2: home=2, guest=1
```

**Comparison Matrix:**

| Home Team | Guest Team | Home's Home | Guest's Guest | Conflict? |
|-----------|------------|-------------|---------------|-----------|
| Team 1 (i=0) | Team 1 (j=0) | 1 | 2 | No |
| Team 1 (i=0) | Team 2 (j=1) | 1 | 1 | **Yes** ✓ |
| Team 2 (i=1) | Team 1 (j=0) | 2 | 2 | **Yes** ✓ |
| Team 2 (i=1) | Team 2 (j=1) | 2 | 1 | No |

**Total Conflicts: 2**

### Test Case 2: n=3

**Input:**
```
Team 1: home=1, guest=2
Team 2: home=2, guest=3
Team 3: home=1, guest=4
```

**Step-by-step iteration:**

```
i=0 (Team 1 as home):
  j=0: 1 vs 2 → No
  j=1: 1 vs 3 → No
  j=2: 1 vs 4 → No

i=1 (Team 2 as home):
  j=0: 2 vs 2 → Yes ✓ (count=1)
  j=1: 2 vs 3 → No
  j=2: 2 vs 4 → No

i=2 (Team 3 as home):
  j=0: 1 vs 2 → No
  j=1: 1 vs 3 → No
  j=2: 1 vs 4 → No
```

**Total Conflicts: 1**

### Test Case 3: n=4 (partial)

**Input:**
```
Team 1: home=100, guest=42
Team 2: home=42, guest=100
```

**Key Conflicts:**
```
Team 1 vs Team 2 (guest): 100 = 100 ✓
Team 2 vs Team 1 (guest): 42 = 42 ✓
```

These mirror conflicts demonstrate the symmetric nature of the problem.

## Complexity Analysis

### Time Complexity

**O(n²)**

* We use two nested loops, each iterating `n` times
* The outer loop runs `n` iterations
* For each outer iteration, the inner loop runs `n` iterations
* Inside the inner loop, we perform a constant-time comparison O(1)
* Total: n × n × O(1) = **O(n²)**

### Space Complexity

**O(n)**

* We store a 2D array `uniforms[n][2]` which requires space for 2n integers
* This simplifies to **O(n)** auxiliary space
* A few integer variables (`count`, loop counters) use O(1) space
* Total: **O(n)**

Note: In some implementations, the array might be allocated on the stack, but the space complexity analysis remains O(n).

## Solution Explanation

The solution uses a straightforward brute force approach:

1. **Data Storage**: A 2D array stores each team's home and guest uniform colors
2. **Exhaustive Checking**: Nested loops examine every possible game scenario
3. **Conflict Detection**: Direct comparison identifies matching colors
4. **Counting**: A simple counter accumulates all conflicts

This approach is optimal for the given constraints (n ≤ 30), as even n² = 900 comparisons execute instantly. The code is clear, maintainable, and directly reflects the problem logic.

## Full Solution

### C++ Implementation

```cpp
#include<iostream>
using namespace std;

int main() {
    // Read the number of teams
    int n;
    cin >> n;
    
    // 2D array to store uniform colors
    // uniforms[i][0] = home uniform color for team i
    // uniforms[i][1] = guest uniform color for team i
    int uniforms[n][2];
    
    // Read uniform colors for all teams
    for(int i = 0; i < n; i++) {
        cin >> uniforms[i][0] >> uniforms[i][1];
    }
    
    // Counter for games with uniform conflicts
    int count = 0;
    
    // Outer loop: iterate through each team as home team
    for(int i = 0; i < n; i++) {
        // Inner loop: iterate through each team as guest team
        for(int j = 0; j < n; j++) {
            // Check if home team's home uniform matches
            // guest team's guest uniform
            if(uniforms[i][0] == uniforms[j][1]) {
                count++;  // Conflict found
            }
        }
    }
    
    // Output the total number of conflicts
    cout << count << endl;
    
    return 0;
}
```

## Test Cases Analysis

| n | Uniform Pattern | Conflict Type | Expected Output |
|---|-----------------|---------------|-----------------|
| 2 | Complete swap (1,2) (2,1) | Full mirror conflicts | 2 |
| 3 | Partial overlap | Some conflicts | 1 |
| 4 | Mixed with duplicates | Multiple conflicts | 3 |
| 2 | No overlap (1,2) (3,4) | No conflicts | 0 |
| 30 | All same colors | Maximum conflicts | 900 (30×30) |

## Edge Cases to Consider

* **Minimum teams**: n=2 (smallest valid input)
* **All identical home uniforms**: Maximum potential conflicts
* **All identical guest uniforms**: Maximum potential conflicts
* **All different colors**: Zero conflicts
* **Same home and guest colors** for a team (e.g., home=5, guest=5)
* **Maximum teams**: n=30 with all possible conflict scenarios

## Common Test Cases

* Teams with mirror uniforms (team A: 1,2 and team B: 2,1)
* Multiple teams sharing the same home uniform color
* Multiple teams sharing the same guest uniform color
* No conflicts at all (completely distinct colors)
* Self-matching scenarios (though teams don't play themselves, the loop includes i=j)

## Common Mistakes to Avoid

* **Comparing wrong indices** - must compare `uniforms[i][0]` with `uniforms[j][1]`, not other combinations
* **Skipping i=j cases** - while teams don't play themselves in reality, the problem counts all comparisons, and skipping would give wrong results
* **Off-by-one errors** in loop bounds - loops should run from 0 to n-1 (or 1 to n with adjusted indexing)

## Interview Relevance

* Tests **nested loop logic** and ability to examine all pair combinations
* Evaluates **array manipulation** and proper indexing
* Assesses understanding of **brute force approaches** and when they're appropriate

## What This Problem Teaches

* Recognizing when brute force is acceptable given constraints
* Understanding ordered pairs vs unordered pairs in comparisons
* Proper 2D array indexing and data organization
* Translating real-world scenarios (sports uniforms) into algorithmic problems

## Key Takeaways

* **Brute force is valid** when the input size is small (n ≤ 30 → n² ≤ 900)
* **Nested loops** naturally represent checking all possible pairings
* **Array indexing discipline** is crucial for correctness
* **Problem constraints** guide algorithm selection - no need for optimization here

## Problem Difficulty Analysis

This is an **Easy-level** problem ideal for beginners. It focuses on:
* Basic nested loop construction
* Array manipulation fundamentals
* Simple counting logic
* Understanding problem requirements

The problem serves as excellent practice for nested iteration patterns and is commonly used in early programming contests to build confidence with multi-dimensional data structures.