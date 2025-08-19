# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
To find the longest common prefix among a list of strings, a natural starting point is to assume the first string itself is the longest common prefix. Then, iterate through this assumed prefix, character by character. At each character position, compare it with the corresponding character in all the other strings in the list. If all other strings have the same character at that position, continue to the next character in the prefix. If a mismatch is found or if the current character position exceeds the length of any other string, then the longest common prefix has been determined, and we return the portion of the assumed prefix up to the last matching character.

# Approach
<!-- Describe your approach to solving the problem. -->
The solution uses a "vertical scanning" or character-by-character comparison approach:

1. **Empty Input:** If the input list strs is empty, there is no common prefix, and an empty string "" is returned.
1. **Initial Prefix:** The first string in the list, strs[0], is the initial candidate for the longest common prefix (prefix). This is a safe starting point because the actual longest common prefix cannot be longer than the shortest string in the input, and strs[0] acts as a reference.
1. **Character Iteration:** An outer for loop iterates through the characters of prefix using the index i. This loop continues for the entire length of prefix.
1. **Character Comparison:** Inside the outer loop, the character char_at_i = prefix[i] is stored. An inner for loop then iterates through the remaining strings in strs (from the second string onwards, using index j from 1 to len(strs) - 1).
1. **Mismatch and Length Check:** For each char_at_i, two conditions are checked within the inner loop:
- Length Check: if i >= len(strs[j]): If the current character index i is greater than or equal to the length of strs[j], it means the current string strs[j] is shorter than the prefix being built. The common prefix cannot extend further than the length of the shortest string in the list.
- Character Mismatch: or strs[j][i] != char_at_i: If the character at index i in strs[j] does not match char_at_i, a mismatch is found.
- If either of these conditions is true, this signifies the end of the longest common prefix. The function immediately returns the substring of prefix from the beginning up to the current index i.
6. **Full Prefix Match:** If the outer loop completes without any return statements, this means all characters of the initial prefix (which was strs[0]) are common among all the strings. In this scenario, the entire prefix is the longest common prefix, and it is returned. 

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**\(O(N\cdot M)\),** where N is the number of strings in the input list strs, and M is the length of the shortest string in the list. In the worst case, the algorithm might compare each character of the shortest string (length M) against all other N - 1 strings. Therefore, in the inner loop, up to N-1 comparisons are made for each character of the shortest string.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**\(O(1)\),** as the algorithm only uses a constant amount of extra space for variables like i, j, char_at_i, and prefix. String slicing operations create new strings, but these are transient and do not scale with the input size in a way that affects the overall auxiliary space complexity significantly.

# Code
```python3 []
class Solution:
    def longestCommonPrefix(self, strs: list[str]) -> str:
        if not strs:
            return ""

        prefix = strs[0]

        for i in range(len(prefix)):
            char_at_i = prefix[i]
            for j in range(1, len(strs)):
                if i >= len(strs[j]) or strs[j][i] != char_at_i:
                    return prefix[:i]
        
        return prefix

```
