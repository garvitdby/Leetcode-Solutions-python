# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
If two identical numbers appear in the list and their indices differ by at most k, we should be able to detect this by keeping track of the most recent index where each number appeared.

Whenever we see a number again, we simply check if the difference between the current index and the previously stored index is at most k.

# Approach
<!-- Describe your approach to solving the problem. -->
1. Create a hash map (index_map) to store the most recent index of each number encountered.

2. Iterate through the list:

- For each number at position index, check if it already exists in the hash map.

- If it does and index - index_map[number] <= k, we found two duplicates within the required distance, so return True.

- Otherwise, update the number's index in the hash map to the current index.

3. If we finish the loop without finding such a pair, return False.

This works because the hash map allows O(1) average-time lookups and updates, so we efficiently track the latest index of each number.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**O(n),** where n is the length of nums, We visit each element exactly once and perform O(1) operations (hash map insert and lookup) for each.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**O(n),** In the worst case (no duplicates or duplicates farther apart than k), we might store all n numbers in the hash map.

# Code
```python3 []
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        index_map = {}

        for index, number in enumerate(nums):
            if number in index_map and index - index_map[number] <= k:
                return True
            index_map[number] = index
        return False
```
