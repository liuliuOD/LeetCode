![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 645. [Set Mismatch](https://leetcode.com/problems/set-mismatch)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findErrorNums(self, nums: List[int]) -> List[int]:
        nums.sort()
        n = len(nums)
        exist = set(nums)
        result = [0, list(set(range(1, n+1))-set(nums))[0]]
        for index in range(n):
            if index+1 < n and nums[index] == nums[index+1]:
                result[0] = nums[index]
                return result
```

Method 2 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findErrorNums(self, nums: List[int]) -> List[int]:
        frequency = defaultdict(int)
        for num in nums:
            frequency[num] += 1

        result = [0, 0]
        for num in range(1, len(nums)+1):
            amount = frequency[num]
            if amount == 1:
                continue

            if amount == 2:
                result[0] = num
            elif amount == 0:
                result[1] = num

        return result
```

Method 3 (Hash Set + Mathematic, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findErrorNums(self, nums: List[int]) -> List[int]:
        n = len(nums)
        sum_unique_nums = sum(set(nums))
        return [sum(nums) - sum_unique_nums, sum(range(1, n+1)) - sum_unique_nums]
```
