# Way Too Long Words

## Platform
**Codeforces**

## Problem Link
[A. Way Too Long Words](https://codeforces.com/problemset/problem/71/A)

## Problem Statement
Sometimes some words like "localization" or "internationalization" are so long that writing them many times in one text is quite tiresome. Let's consider a word too long if its length is strictly more than 10 characters. All too long words should be replaced with a special abbreviation.

The abbreviation is made like this: write down the first and the last letters of a word, and between them write the number of letters between the first and the last letters. That number is in decimal system and doesn't contain any leading zeroes.

Thus, "localization" will be spelt as "l10n", and "internationalization" will be spelt as "i18n".

You are suggested to automatize the process of changing the words with abbreviations. At that all too long words (length > 10) should be replaced by the abbreviation and the words that are not too long should not undergo any changes.

## Input Format
The first line contains an integer `t` (1 ≤ t ≤ 100) — the number of words.

Each of the following `t` lines contains one word. All the letters are lowercase Latin letters and each word's length is between 1 and 100 characters, inclusive.

## Output Format
Print `t` lines. The i-th line should contain the result of replacing the i-th word from the input data.

## Constraints
- 1 ≤ t ≤ 100
- 1 ≤ length of each word ≤ 100
- All letters are lowercase Latin letters

## Examples

### Example 1
**Input:**
```
4
word
localization
internationalization
pneumonoultramicroscopicsilicovolcanoconiosis
```

**Output:**
```
word
l10n
i18n
p43s
```

**Explanation:**
- "word" has length 4 (≤ 10), so it remains unchanged
- "localization" has length 12 (> 10), so it becomes "l" + 10 + "n" = "l10n"
- "internationalization" has length 20 (> 10), so it becomes "i" + 18 + "n" = "i18n"
- "pneumonoultramicroscopicsilicovolcanoconiosis" has length 45 (> 10), so it becomes "p" + 43 + "s" = "p43s"

### Example 2
**Input:**
```
3
a
ab
abcdefghij
```

**Output:**
```
a
ab
abcdefghij
```

**Explanation:**
- "a" has length 1 (≤ 10), remains unchanged
- "ab" has length 2 (≤ 10), remains unchanged
- "abcdefghij" has length 10 (≤ 10), remains unchanged (exactly 10 is not "too long")

### Example 3
**Input:**
```
2
abcdefghijk
substitution
```

**Output:**
```
a9k
s10n
```

**Explanation:**
- "abcdefghijk" has length 11 (> 10), becomes "a" + 9 + "k" = "a9k"
- "substitution" has length 12 (> 10), becomes "s" + 10 + "n" = "s10n"

## Approach
**String Manipulation / Implementation**

## Intuition
The problem is straightforward: we need to abbreviate words that are too long (length > 10). The key insight is that we only need three pieces of information to create the abbreviation:
1. The first character of the word
2. The count of characters between the first and last character (length - 2)
3. The last character of the word

If a word has 10 or fewer characters, we simply output it as is. This is a simple conditional check followed by string manipulation.

## Algorithm Steps
1. Read the number of test cases `t`
2. For each test case:
   - Read the word `s`
   - Calculate the length `n` of the word
   - If `n > 10`:
     - Create abbreviation: first character + (n - 2) + last character
   - Else:
     - Keep the word unchanged
   - Print the result

## Visual Walkthrough

Let's visualize the abbreviation process for the word "localization":

```
Original word: l o c a l i z a t i o n
Position:      0 1 2 3 4 5 6 7 8 9 10 11
               ↓                       ↓
            first                    last

Length = 12
Characters between first and last = 12 - 2 = 10

Result: l + 10 + n = "l10n"
```

For the word "word":
```
Original word: w o r d
Position:      0 1 2 3

Length = 4 (≤ 10)
Result: "word" (unchanged)
```

## Complexity Analysis

### Time Complexity
**O(t × m)** where:
- `t` is the number of test cases
- `m` is the average length of words

For each word, we perform constant time operations (checking length, accessing first/last character, string concatenation). Reading the input takes O(m) time per word.

### Space Complexity
**O(m)** where:
- `m` is the maximum length of a word

We store each word temporarily. The abbreviated form is always shorter than or equal to the original word (maximum 3 characters for length up to 100).

## Solution Explanation

The solution uses a simple conditional approach:

1. **Input Reading**: Read the number of test cases, then iterate through each word
2. **Length Check**: For each word, check if its length exceeds 10
3. **Abbreviation Logic**: 
   - If length > 10: construct a new string with first character, middle count (length - 2), and last character
   - If length ≤ 10: keep the original word
4. **Output**: Print the result for each word

The key operations are:
- `s.charAt(0)` or `s[0]`: Get the first character
- `s.charAt(n-1)` or `s[n-1]`: Get the last character
- `(n - 2)`: Calculate the count of middle characters
- String concatenation to form the abbreviation

## Full Solution

### Java Implementation
```java
import java.util.Scanner; 

public class A_Way_Too_Long_Words { 
    public static void main(String[] args) { 
        Scanner sc = new Scanner(System.in); 
        
        // Read number of test cases
        int t = sc.nextInt(); 
        
        // Process each word
        while(t-- > 0) { 
            String s = sc.next(); // Read the word
            int n = s.length();   // Get word length
            
            // If word is too long (> 10 characters), abbreviate it
            if(n > 10) {
                // Create abbreviation: first_char + middle_count + last_char
                s = "" + s.charAt(0) + (n - 2) + s.charAt(n - 1); 
            }
            
            // Print the result (abbreviated or original)
            System.out.println(s); 
        } 
    } 
}
```

### C++ Implementation
```cpp
#include <iostream>
using namespace std;

int main() {
    int t;
    cin >> t; // Read number of test cases
    
    while(t--) {
        string s;
        cin >> s; // Read the word
        int n = s.size(); // Get word length
        
        // If word is too long (> 10 characters), abbreviate it
        if(n > 10) {
            // Create abbreviation: first_char + middle_count + last_char
            s = s[0] + to_string(n - 2) + s[n - 1];
        }
        
        // Print the result (abbreviated or original)
        cout << s << '\n';
    }
    
    return 0;
}
```

## Test Cases Analysis

| Input | Length | Condition | Output | Explanation |
|-------|--------|-----------|--------|-------------|
| word | 4 | ≤ 10 | word | Short word, no change |
| localization | 12 | > 10 | l10n | First char + 10 middle + last char |
| internationalization | 20 | > 10 | i18n | First char + 18 middle + last char |
| a | 1 | ≤ 10 | a | Single character, no change |
| abcdefghij | 10 | = 10 | abcdefghij | Exactly 10 chars, no change |
| abcdefghijk | 11 | > 10 | a9k | First char + 9 middle + last char |
| pneumonoultramicroscopicsilicovolcanoconiosis | 45 | > 10 | p43s | Very long word abbreviated |

## Edge Cases to Consider

1. **Minimum Length (1 character)**: Single letter words should remain unchanged
2. **Boundary Case (10 characters)**: Words with exactly 10 characters should NOT be abbreviated (condition is strictly greater than 10)
3. **Boundary Case (11 characters)**: Words with exactly 11 characters should be abbreviated
4. **Maximum Length (100 characters)**: Should handle the maximum constraint properly
5. **All Same Characters**: Words like "aaaaaaaaaaaaa" should still be abbreviated correctly
6. **Two Character Words**: Should remain unchanged as they are ≤ 10

## Common Test Cases

1. **Very short words** (length 1-3): No abbreviation needed
2. **Words at threshold** (length 10): Should remain unchanged
3. **Words just over threshold** (length 11): Should be abbreviated to pattern like "a9z"
4. **Very long words** (length 50-100): Large middle count numbers
5. **Multiple test cases**: Ensure loop handles all inputs correctly

## Common Mistakes to Avoid

1. **Off-by-one Error**: Using `n > 11` or `n >= 10` instead of `n > 10` for the condition check
2. **Incorrect Middle Count**: Calculating `n - 1` or `n` instead of `n - 2` for the middle character count
3. **String Indexing**: Forgetting that the last character is at index `n - 1`, not `n`

## Interview Relevance

1. **String Manipulation Fundamentals**: Tests basic string operations like accessing characters and concatenation
2. **Boundary Condition Handling**: Requires careful attention to the "strictly greater than 10" condition
3. **Clean Implementation**: Simple problem that should be solved quickly and correctly, showing coding efficiency

## What This Problem Teaches

- Basic string manipulation techniques
- Importance of reading problem constraints carefully (> 10, not ≥ 10)
- String concatenation and character access in different programming languages
- Input/output handling for competitive programming
- How to optimize text representation (compression concept)

## Key Takeaways

- Always check boundary conditions carefully (= vs > vs ≥)
- String indexing: first character at index 0, last at length - 1
- The middle count formula is length - 2 (excluding first and last)
- Simple problems can still catch you with edge cases
- Efficient I/O handling is important in competitive programming

## Problem Difficulty Analysis

**Difficulty Level**: Easy (Codeforces Rating: 800)

**Skills Required**:
- Basic string operations
- Conditional logic
- Simple arithmetic

**Why It's Beginner-Friendly**:
- Clear problem statement
- Straightforward logic
- No complex data structures needed
- Good introduction to competitive programming
- Teaches attention to detail with constraints

**Time to Solve**: 5-10 minutes for beginners, 2-3 minutes for experienced programmers