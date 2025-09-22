# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem asks whether two strings, s and t, are isomorphic. This means that a one-to-one mapping exists between the characters of s and t, preserving the order of the characters. For example, egg and add are isomorphic because 'e' maps to 'a' and 'g' maps to 'd', and this mapping is consistent throughout both strings.

To solve this, a mapping must be established and consistently maintained from s to t and from t to s. Two hash maps are a suitable data structure for this task. One hash map (mapST) will store the mapping from characters in s to characters in t, and the other (mapTS) will store the reverse mapping from t to s.
 
The core logic is to iterate through both strings simultaneously and verify that for each pair of characters (c1, c2):
1. If c1 is already in mapST, its mapped value must be c2.
2. If c2 is already in mapTS, its mapped value must be c1.
3. If neither c1 nor c2 has been seen before, a new consistent mapping is established.

# Approach
<!-- Describe your approach to solving the problem. -->
The solution uses two hash maps (mapST and mapTS) to track the character mappings and a single loop to iterate through the strings.

1. **Length Check:** An initial check ensures that the lengths of s and t are equal. If not, they cannot be isomorphic, so False is returned immediately.

2. **Initialize Hash Maps:** Two empty hash maps, mapST and mapTS, are created to store the forward (s -> t) and reverse (t -> s) mappings.
3. **Iterate and Validate Mappings:**
A for loop iterates through the strings s and t simultaneously using zip.
- **Forward Mapping (s to t):**
1. Checks if c1 (character from s) is already in mapST.
2. If it is, it verifies if the existing mapping (mapST[c1]) is consistent with the current character c2. If not, it returns False.
3. If c1 is not in mapST, it establishes a new mapping: mapST[c1] = c2.
- **Reverse Mapping (t to s):**
1. Performs a similar check for the reverse mapping using mapTS and c2 (character from t). This is crucial to ensure a one-to-one mapping (e.g., handles cases like s = "foo", t = "bar" where f -> b, o -> a, o -> r is an invalid mapping).
2. Checks if c2 is in mapTS.
3. If it is, it verifies if the existing reverse mapping (mapTS[c2]) is consistent with c1. If not, it returns False.
4. If c2 is not in mapTS, it establishes a new reverse mapping: mapTS[c2] = c1.

4. **Return True:** If the loop completes without finding any inconsistencies, the strings are isomorphic, and the function returns True.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**\(O(N)\),** where \(N\) is the length of the strings. The solution iterates through the strings only once. The hash map operations (in, [], len) have an average time complexity of **\(O(1)\)**

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**\(O(K)\),** where \(K\) is the number of unique characters in the strings. In the worst case (e.g., all characters are unique), the hash maps will store up to **\(2K\)** entries, which is bounded by the size of the alphabet (e.g., 256 for ASCII). Therefore, the space complexity is effectively constant.

# Code
```python3 []
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        mapST, mapTS = {}, {}

        for c1, c2 in zip(s, t):
            if c1 in mapST:
                if mapST[c1] != c2:
                    return False

            else:
                mapST[c1] = c2

            if c2 in mapTS:
                if mapTS[c2] != c1:
                    return False

            else:
                mapTS[c2] = c1

        return True
```
