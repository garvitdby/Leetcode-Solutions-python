# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
One pointer (let's call it i) iterates through the array, and the other (k) keeps track of the index where the next unique element should be placed. Since the array is sorted, you only need to compare each element with the previous one. If they are different, it's a unique element, and you place it at the kth position, incrementing k. If they are the same, you skip it, effectively removing the duplicate. 

# Approach
<!-- Describe your approach to solving the problem. -->
Two Pointers

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
O(n) as we only traverse the array once

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
O(1) because only constant amount of extra space is used

# Code
```python3 []
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if not nums:
            return 0

        start = 0
        for end in range(1, len(nums)):
            if nums[end] != nums[end - 1]:
                start += 1
                nums[start] = nums[end]
        return start + 1
        
```
