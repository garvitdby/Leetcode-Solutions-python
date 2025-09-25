# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
Anagrams are words that contain exactly the same characters with the same frequencies, just arranged differently.

So if we can create a signature that uniquely represents the frequency of each letter in a word, then all anagrams will share the same signature.

# Approach
<!-- Describe your approach to solving the problem. -->
1. **Frequency Signature:**
- For each string, create a list of size 26 (for each letter a–z) initialized with zeros.
- Increment the count at the appropriate position for every character in the string.

2. **Hashable Key:**
- Convert the list of counts into a tuple (since lists cannot be dictionary keys).
- This tuple acts as a unique key for all anagrams.

3. **Group in Dictionary:**
- Use a dictionary (result) where the key is the tuple of character counts and the value is a list of all words with that signature.

4. After processing all strings, return the list of grouped anagrams (result.values()).

This method groups anagrams in a single pass while using a simple fixed-size frequency array.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**O(n . k),** Let n be the number of strings and k be the maximum length of a single string.
- For each string, counting character takes O(k)
- Dictionary operations are O(1) on average

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**O(n.k)**, for the output and keys. The extra space for counts per string is O(26) = O(1) per iteration
- We store a frequency array of size 26 for each key (as a tuple), but the total number of unique keys is at most n.
- The output itself contains all the strings.

# Code
```python3 []
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        result = {}

        for s in strs:
            count = [0] * 26

            for char in s:
                count[ord(char) - ord('a')] += 1

            ctuple = tuple(count)

            if ctuple not in result:
                result[ctuple] = []
            result[ctuple].append(s)

        return list(result.values())
```
