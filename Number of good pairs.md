# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem asks for the number of pairs (i, j) where i < j and nums[i] == nums[j]. A brute-force approach would use nested loops to check every possible pair, which would be inefficient for large inputs. 

A more optimal approach is to count the frequency of each number in the array. Once we know how many times each number appears, we can use a combinatorial formula to calculate the number of identical pairs. If a number appears c times, the number of ways to choose two indices from these c occurrences is given by the combination formula "c choose 2", which is c * (c - 1) / 2. By summing this value for every unique number, we can find the total number of identical pairs.

# Approach
<!-- Describe your approach to solving the problem. -->
The solution implements the frequency-counting approach using Python's collections.Counter.
1. **Count Frequencies:** First, a Counter is used to efficiently count the occurrences of each number in the input list nums. This results in a hash map where keys are the numbers and values are their frequencies.
2. **Calculate Pairs:** The code then iterates through the values (the frequencies) of the Counter object.
3. **Combinatorial Sum:** For each frequency c, it calculates c * (c - 1) // 2, which is the number of ways to choose 2 items from c items. This result is added to a running total, res.
4. **Return:** After iterating through all the unique numbers, res will hold the total number of identical pairs, which is then returned.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**\(O(N)\),** where \(N\) is the number of elements in the nums array. The dominant operation is creating the Counter object, which requires a single pass through the input list. The subsequent loop over unique items is at most.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**\(O(U)\),** where \(U\) is the number of unique elements in nums. The Counter object stores the frequency of each unique element. In the worst case, all elements are unique, and the space complexity becomes **\(O(N)\)**

# Code
```python3 []
class Solution:
    def numIdenticalPairs(self, nums: List[int]) -> int:
        count = Counter(nums)
        res = 0

        for n, c in count.items():
            res += c * (c - 1) // 2
        
        return res
```
