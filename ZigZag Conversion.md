# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The core idea behind this problem is to simulate the way the characters would be placed in the zigzag pattern. We can imagine having a separate "bucket" or string for each row in the zigzag. As we iterate through the input string, we determine which row the current character belongs to and append it to that row's string. The direction of movement (down or up the rows) changes when we hit the top or bottom row.

# Approach
<!-- Describe your approach to solving the problem. -->
1. **Handle Edge Case:** If numRows is 1, the zigzag conversion has no effect, so the original string s can be returned directly.
Initialize Data Structure: Create a list of empty lists (or strings) named rows, where the number of inner lists equals numRows. Each inner list will store the characters belonging to that particular row.
2. **Simulate Zigzag Traversal:**
- Initialize i (current row index) to 0 and d (direction) to 1 (initially moving downwards).
- Iterate through each char in the input string s.
- Append char to rows[i].
3. **Change Direction:**
- If i is 0 (top row), set d to 1 (move downwards).
- Else if i is numRows - 1 (bottom row), set d to -1 (move upwards).
- Update i by adding d (i += d).
4. **Combine Rows:** After processing all characters, initialize an empty string res. Iterate through the rows list and join the characters within each inner list (converting them into strings) and append them to res.
5. **Return Result:** Return the final res string.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**\(O(N)\),** where N is the length of the input string s. This is because the code iterates through the string once to place the characters into the rows and then iterates through the rows list to join them, with string joining potentially taking additional time proportional to the length of the string.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**\(O(N)\),** where N is the length of the input string s. A list of lists (rows) is created to store the characters, and in the worst case (e.g., when numRows equals 1), the combined length of strings in rows will be equal to N.

# Code
```python3 []
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows == 1:
            return s
        
        i = 0
        d = 1
        rows = [[] for _ in range(numRows)]

        for char in s:
            rows[i].append(char)
            if i == 0:
                d = 1
            elif i == numRows - 1:
                d = -1
            i += d
        
        res = ''
        for i in range(numRows):
            res += ''.join(rows[i])

        return res
```
