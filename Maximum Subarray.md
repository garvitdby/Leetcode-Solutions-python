# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem asks for the maximum sum of a contiguous subarray within a given array of numbers. A brute-force approach would involve checking every possible subarray, which would be inefficient. A more optimal solution, known as Kadane's Algorithm, uses a dynamic programming approach. 

The core idea is to iterate through the array and keep track of two values:
max_current: The maximum sum of a subarray ending at the current position.
max_global: The maximum sum found so far across the entire array. 
At each step, the algorithm decides whether to extend the current subarray by adding the next number or to start a new subarray with the current number. It chooses the path that yields a larger sum for max_current. The max_global value is updated whenever a new maximum max_current is found.

# Approach
<!-- Describe your approach to solving the problem. -->
The solution implements Kadane's algorithm using a single pass through the input array nums.
1. **Initialization:**
- max_current is initialized to the first element of the array, nums[0]. This variable will store the maximum sum of a contiguous subarray ending at the current index.
- max_global is also initialized to nums[0]. This variable will store the overall maximum sum found so far.
2. **Iteration:**
- A for loop iterates through the rest of the array, starting from the second element (index 1).
- Inside the loop, max_current is updated. At each element nums[i], the new max_current is the maximum of two values:
- nums[i]: Starting a new subarray from the current element.
- max_current + nums[i]: Extending the previous subarray by adding the current element.
- After updating max_current, max_global is updated to be the maximum of the current max_current and the existing max_global. This ensures that max_global always holds the highest sum found so far.
3. **Return Value:**
After the loop finishes, max_global will hold the maximum sum of any contiguous subarray. The function returns this value. 

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
\(O(n)\), where n is the number of elements in the nums array. The algorithm performs a single pass through the array, with a constant amount of work done at each element.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
\(O(1)\), as the algorithm uses only a few variables (max_current, max_global, and the loop counter i) to store its state, regardless of the input size.

# Code
```python3 []
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        max_current = nums[0]
        max_global = nums[0]

        for i in range(1, len(nums)):
            max_current = max(nums[i], max_current + nums[i])
            max_global = max(max_current, max_global)
        return max_global
```
