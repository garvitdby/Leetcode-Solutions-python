# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
One pointer (let's call it start) tracks the position to place the next non-zero element, while the other pointer iterates through the entire array. When a non-zero element is encountered, it's swapped with the element at the start index, and then start index is incremented. 

# Approach
<!-- Describe your approach to solving the problem. -->
Two Pointers

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
(O(n)), because we pass through the array exactly once

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
(O(1)) as no additional list is used, thus achieving in-place rearrangement.

# Code
```python3 []
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        start = 0
        for end in range(len(nums)):
            if nums[end] != 0:
                nums[start], nums[end] = nums[end], nums[start]
                start += 1
        return nums
        
```
