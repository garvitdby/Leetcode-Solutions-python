# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
**Sorting:** Just sort the array and return the elements in array which are occuring more than len(nums) // 2
**Boyer Moore Voting Algorithm:** Imagine each non-majority element "canceling out" one instance of the majority element. Since the majority element appears more than half the time, there will always be a surplus of the majority element, even after all possible cancellations. This surplus guarantees that the majority element will be the one remaining as the candidate at the end of the process.

# Approach
<!-- Describe your approach to solving the problem. -->
1. Sorting
2. Boyer Moore Voting Algorithm

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**Sorting:** O(nlogn), Because of sorting algorithm
**Boyre Moore Voting Algorithm:** O(n), Single pass over the list to calculate candidate majority 
- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**Sorting:** O(1), python built in sorting method may acquire space
**Boyre Moore Voting Algorithm:** O(1), independent of input zide, works only with few variables.

# Code
```python3 []
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        # using sorting
        # nums.sort()
        # return nums[len(nums) // 2]

        # Boyer Moore voting algorithm
        result, count = 0, 0

        for i in nums:
            if count == 0:
                result = i
            count += (1 if i == result else -1)
        return result


```
