# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The core idea is to efficiently check if the "other half" of the target sum exists among previously seen numbers. A hash map allows for nearly instant lookups, avoiding a slow, repeated search through the array for each number.

# Approach
<!-- Describe your approach to solving the problem. -->
 Iterate through the array once, calculate the complement for each number, check if the complement is in the hash map, and if not, add the current number and its index to the hash map.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
O(n), as it iterates through array once

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
O(n), as the amount of extra space required grows linearly with the size of the input array n

# Code
```python3 []
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hash_map = {}
        for i in range(len(nums)):
            num = nums[i]
            comp = target - num

            if comp in hash_map:
                return (hash_map[comp], i)

            hash_map[num] = i

```
