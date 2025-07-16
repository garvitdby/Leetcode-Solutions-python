# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The core idea is to maintain a window of valid elements (at most two occurrences) and overwrite the original array with elements from that window

# Approach
<!-- Describe your approach to solving the problem. -->
Two Pointers with counter

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
O(n), as algorith iterates through the array once and inner if else statement take constant time

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
O(1), as no extra space is used because it modifies array in place

# Code
```python3 []
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        start, end = 0, 0

        while end < len(nums):
            count = 1
            while end + 1 < len(nums) and nums[end] == nums[end + 1]:
                end += 1
                count += 1

            for i in range(min(2, count)):
                nums[start] = nums[end]
                start += 1
            end += 1
        return start

```
