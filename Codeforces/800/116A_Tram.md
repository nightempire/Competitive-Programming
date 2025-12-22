# A. Tram

## Platform

Codeforces

## Problem Link

[A. Tram](https://codeforces.com/problemset/problem/116/A)

## Problem Statement

A tram moves along a route with several stops.

At each stop:

* Some passengers **leave** the tram.
* Some passengers **enter** the tram.

The tram starts empty.
Your task is to determine the **minimum capacity** the tram must have so that it never exceeds its capacity during the journey.

## Input Format

* The first line contains an integer `n`, the number of tram stops.
* The next `n` lines each contain two integers:

  * `a` — number of passengers leaving the tram
  * `b` — number of passengers entering the tram

## Output Format

Print a single integer representing the **maximum number of passengers** that were on the tram at any point.

## Constraints

* `1 ≤ n ≤ 1000`
* `0 ≤ a, b ≤ 1000`
* The number of passengers never becomes negative

## Examples

### Example 1

Input

```
4
0 3
2 5
4 2
4 0
```

Explanation

Stop-by-stop passenger count:

* Stop 1: 0 − 0 + 3 = 3
* Stop 2: 3 − 2 + 5 = 6
* Stop 3: 6 − 4 + 2 = 4
* Stop 4: 4 − 4 + 0 = 0

Maximum passengers at any stop = `6`

Output

```
6
```

### Example 2

Input

```
2
0 10
5 0
```

Explanation

* Stop 1: 10 passengers
* Stop 2: 5 passengers

Maximum capacity required = `10`

Output

```
10
```

## Approach

Simulation with running maximum tracking.

The tram’s passenger count is updated at every stop, and the maximum value encountered is stored.

## Intuition

The tram capacity must be **at least as large as the highest number of passengers present at any moment**.

By simulating each stop:

* Subtract passengers leaving
* Add passengers entering
* Update the maximum observed passenger count

The highest value encountered during the simulation is the answer.

## Algorithm Steps

* Read the number of stops `n`
* Initialize `capacity` and `maxCapacity` to `0`
* For each stop:

  * Read values `a` and `b`
  * Update current capacity as `capacity = capacity - a + b`
  * Update `maxCapacity` if current capacity is greater
* Output `maxCapacity`

## Visual Walkthrough

Example input:

```
0 3
2 5
```

Passenger count progression:

```
Start: 0
After stop 1: 0 + 3 = 3
After stop 2: 3 - 2 + 5 = 6
```

Maximum encountered passengers = `6`

## Complexity Analysis

### Time Complexity

**O(n)**
Each stop is processed exactly once.

### Space Complexity

**O(1)**
Only a few integer variables are used.

## Solution Explanation

The solution performs a linear scan through the tram stops, maintaining a running count of passengers.

At every stop, passengers leaving are subtracted first, followed by adding passengers entering. The current passenger count is then compared with the maximum observed so far.

This ensures that the final result represents the minimum required tram capacity.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of tram stops
    int n;

    // Current number of passengers in the tram
    int capacity = 0;

    // Maximum number of passengers observed
    int maxCapacity = 0;

    // Read number of stops
    cin >> n;

    // Process each stop
    while (n--) {

        int a, b;
        cin >> a >> b;

        // Update current capacity
        capacity = capacity - a + b;

        // Update maximum capacity if needed
        maxCapacity = capacity > maxCapacity ? capacity : maxCapacity;
    }

    // Output the required tram capacity
    cout << maxCapacity << endl;

    return 0;
}
```

## Test Cases Analysis

| Stops | Passenger Changes | Expected Output |
| ----: | ----------------- | --------------- |
|     1 | 0 5               | 5               |
|     2 | 0 3, 1 2          | 4               |
|     4 | Mixed             | Maximum value   |
|  1000 | Large input       | Valid maximum   |

## Edge Cases to Consider

* Only one stop
* No passengers entering at any stop
* Maximum passengers entering at the same stop

## Common Test Cases

* Gradual increase in passengers
* Sudden spike in passengers
* All passengers leaving at final stop

## Common Mistakes to Avoid

* Forgetting to subtract passengers before adding new ones
* Not tracking the maximum value
* Assuming final passenger count equals required capacity

## Interview Relevance

* Demonstrates simulation techniques
* Tests ability to track running maximums
* Common logic-based interview problem

## What This Problem Teaches

* Translating real-world scenarios into simulations
* Importance of tracking intermediate values
* Efficient use of variables without extra memory

## Key Takeaways

* Capacity problems often require tracking peak usage
* Simulation can be both simple and powerful
* Always consider intermediate states, not just final results

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic arithmetic operations and logical tracking, making it suitable for beginners and technical interview preparation.
