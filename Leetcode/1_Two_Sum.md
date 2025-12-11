# Two Sum

## Platform
**LeetCode**

## Problem Link
[1. Two Sum](https://leetcode.com/problems/two-sum/)

## Problem Statement
Given an array of integers `nums` and an integer `target`, return the **indices** of the two numbers such that they add up to `target`.

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

You can return the answer in any order.

## Input Format
- `nums`: An array of integers (2 ≤ nums.length ≤ 10⁴)
- `target`: An integer (-10⁹ ≤ target ≤ 10⁹)

## Output Format
Return an array of two integers representing the indices of the two numbers that add up to the target.

## Constraints
- 2 ≤ nums.length ≤ 10⁴
- -10⁹ ≤ nums[i] ≤ 10⁹
- -10⁹ ≤ target ≤ 10⁹
- **Only one valid answer exists**

## Example

### Example 1
**Input:** 
```
nums = [2, 7, 11, 15]
target = 9
```
**Output:** 
```
[0, 1]
```
**Explanation:** nums[0] + nums[1] = 2 + 7 = 9

### Example 2
**Input:** 
```
nums = [3, 2, 4]
target = 6
```
**Output:** 
```
[1, 2]
```
**Explanation:** nums[1] + nums[2] = 2 + 4 = 6

### Example 3
**Input:** 
```
nums = [3, 3]
target = 6
```
**Output:** 
```
[0, 1]
```
**Explanation:** nums[0] + nums[1] = 3 + 3 = 6

---

# Approach 1: Hash Map (Optimal Solution)

## Intuition
Instead of checking every pair of numbers, we can use a hash map to store numbers we've seen along with their indices. For each number, we check if its complement (target - current number) exists in the map.

## Algorithm
1. Create a hash map to store (value → index) pairs
2. Iterate through the array:
   - Calculate complement: `x = target - nums[i]`
   - Check if complement exists in the map
   - If yes: return the stored index and current index
   - If no: store current number and its index in the map
3. Return result

## Complexity Analysis
- **Time Complexity**: O(n) — single pass through the array, with O(1) hash map operations
- **Space Complexity**: O(n) — storing up to n elements in the hash map

## Implementation

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        // Hash map to store (number -> index)
        Map<Integer, Integer> map = new HashMap<>();
        
        // Iterate through array
        for(int i = 0; i < nums.length; i++) {
            // Calculate complement needed to reach target
            int x = target - nums[i];
            
            // Check if complement exists in map
            if(map.containsKey(x)) {
                // Found the pair! Return indices
                return new int[] {map.get(x), i};
            }
            
            // Store current number and its index for future lookups
            map.put(nums[i], i);
        }
        
        // This line should never be reached (problem guarantees solution exists)
        return new int[] {0, 0};
    }
}
```

## Step-by-Step Example

**Input:** nums = [2, 7, 11, 15], target = 9

```
Iteration 0: i=0, nums[0]=2
- Complement: x = 9 - 2 = 7
- Map: {} (empty)
- 7 not in map
- Add to map: {2: 0}

Iteration 1: i=1, nums[1]=7
- Complement: x = 9 - 7 = 2
- Map: {2: 0}
- 2 found in map! ✓
- Return [0, 1]
```

## Why This Works
- We check if the complement exists **before** adding the current number
- This prevents using the same element twice
- One-pass solution is possible because we build the lookup table as we go

---

# Approach 2: Nested Loop (Brute Force)

## Intuition
Check every possible pair of numbers by using two nested loops. For each element, check if it forms a valid pair with any subsequent element.

## Algorithm
1. Use outer loop starting from index 1
2. For each outer index `i`, use inner loop from `i` to end
3. Check if `nums[j] + nums[j - i] == target`
4. If match found, return the pair of indices
5. Continue until pair is found

## Complexity Analysis
- **Time Complexity**: O(n²) — nested loops checking all pairs
- **Space Complexity**: O(1) — no extra space needed

## Implementation

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        // Outer loop: represents the gap between indices
        for(int i = 1; i < nums.length; i++) {
            // Inner loop: check all pairs with gap i
            for(int j = i; j < nums.length; j++) {
                // Check if current element + element at distance i equals target
                if(nums[j] + nums[j - i] == target) {
                    return new int[] {j, j - i};
                }
            }
        }
        
        // This line should never be reached (problem guarantees solution exists)
        return new int[] {0, 0};
    }
}
```

## Step-by-Step Example

**Input:** nums = [2, 7, 11, 15], target = 9

```
i=1 (gap of 1):
- j=1: nums[1] + nums[0] = 7 + 2 = 9 ✓
- Return [1, 0] (or [0, 1] after reordering)

No need to continue!
```

## How This Approach Works
- `i` represents the distance/gap between two indices
- `j` is the current position
- `j - i` is the position at distance `i` before `j`
- This cleverly avoids checking the same pair twice

---

# Comparison of Approaches

| Aspect | Hash Map (Approach 1) | Nested Loop (Approach 2) |
|--------|----------------------|--------------------------|
| **Time Complexity** | O(n) ✓ | O(n²) |
| **Space Complexity** | O(n) | O(1) ✓ |
| **Readability** | High ✓ | Medium |
| **Efficiency** | Optimal for large inputs ✓ | Good for small inputs |
| **Interview Preference** | Preferred ✓ | Shows brute force understanding |

## When to Use Each Approach

**Hash Map (Approach 1)**:
- ✓ Large input arrays
- ✓ When time complexity is critical
- ✓ Interview/production code
- ✓ When O(n) space is acceptable

**Nested Loop (Approach 2)**:
- ✓ Small input arrays
- ✓ When space is extremely limited
- ✓ As a starting point to show problem understanding
- ✓ Educational purposes

---

# Key Insights

1. **Hash Map Power**: Trading space for time — O(n) space gives us O(n) time
2. **Complement Search**: Instead of finding two numbers that sum to target, find one number and check if its complement exists
3. **One-Pass Solution**: We don't need to populate the entire map first; build it as we go
4. **Index Awareness**: Store indices, not just values, since we need to return positions
5. **Duplicate Handling**: The approach naturally handles duplicates by checking complement before insertion

## Common Mistakes to Avoid

1. **Using same element twice**: Check complement before adding current element
2. **Off-by-one errors**: Be careful with loop boundaries
3. **Integer overflow**: Not an issue in this problem, but be aware for large numbers
4. **Assuming sorted array**: Don't sort! We need to return original indices
5. **Not handling duplicates**: Hash map approach handles this elegantly

## Follow-Up Questions

1. **What if we need to find all pairs?** — Continue searching instead of returning immediately
2. **What if no solution exists?** — Current problem guarantees solution, but add validation in real scenarios
3. **Can we do it in O(1) space with O(n) time?** — Not possible without modifying input or additional constraints
4. **What if array is sorted?** — Two-pointer approach would work in O(n) time, O(1) space

---

# Practice Tips

1. **Start with brute force**: Show understanding, then optimize
2. **Explain trade-offs**: Time vs space complexity
3. **Test edge cases**: [3,3] with target=6, negative numbers, zeros
4. **Communicate**: Explain your thought process while coding
5. **Ask clarifications**: Can array be modified? Are there duplicate solutions?

---

**Note**: This is one of the most popular interview questions. The hash map approach demonstrates fundamental problem-solving skills: recognizing when to trade space for time, and how hash tables enable O(1) lookups to optimize algorithms.