# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem of finding the maximum subarray sum in a circular array can be broken down into two cases:
1. **The maximum subarray is non-circular:** This is the classic maximum subarray sum problem, which can be solved efficiently with Kadane's algorithm. The subarray does not wrap around the end of the array.

2. **The maximum subarray is circular:** The subarray wraps around from the end of the array to the beginning. The sum of this wrapping subarray is equivalent to the total sum of the array minus the minimum subarray sum. By removing the minimum sum segment, we are left with the maximum sum segment.

The final answer will be the maximum of these two cases. A special edge case must be handled: if all numbers in the array are negative, the minimum subarray sum is the total sum, and total_sum - min_global would incorrectly return 0. In this scenario, the standard maximum subarray sum (which would be the largest negative number) is the correct answer. The check if max_global > 0 handles this edge case.

# Approach
<!-- Describe your approach to solving the problem. -->
The solution adapts Kadane's algorithm to find both the maximum and minimum subarray sums in a single pass.
1. **Initialization:**
- Initialize max_global and min_global with the first element of the array. These will store the final maximum and minimum subarray sums.
- Initialize max_current and min_current to 0. These will track the sum of the current contiguous subarray for both maximum and minimum sums.
- Initialize total_sum to 0 to accumulate the sum of all elements.

2. **Single Pass Iteration:**
- Loop through each number nums[i] in the array.
- **Calculate Maximum Sum:** Update max_current by taking the maximum of nums[i] (starting a new subarray) and nums[i] + max_current (extending the current subarray).
- **Calculate Minimum Sum:** Update min_current by taking the minimum of nums[i] (starting a new subarray) and nums[i] + min_current (extending the current subarray).
- **Update Global Sums:** Update max_global and min_global with the maximum and minimum values found so far.
Accumulate Total Sum: Add nums[i] to total_sum.

3. **Return Value:**
- Return the maximum of max_global (for the non-circular case) and total_sum - min_global (for the circular case).
- A check if max_global > 0 is added to handle the edge case where all numbers are negative. In this case, max_global (the largest negative number) is the answer, and total_sum - min_global would be 0, which is incorrect.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**\(O(N)\),** where \(N\) is the number of elements in nums. The solution iterates through the array once to compute all necessary sums.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**\(O(1)\),** as the algorithm uses a fixed number of variables regardless of the input array's size.

# Code
```python3 []
class Solution:
    def maxSubarraySumCircular(self, nums: List[int]) -> int:
        max_global, min_global = nums[0],  nums[0]
        max_current, min_current = 0, 0
        total_sum = 0

        for i in range(len(nums)):
            max_current = max(nums[i], nums[i] + max_current)
            min_current = min(nums[i], nums[i] + min_current)
            total_sum += nums[i]
            max_global = max(max_global, max_current)
            min_global = min(min_current, min_global)

        return max(max_global, total_sum - min_global) if max_global > 0 else max_global 
```
