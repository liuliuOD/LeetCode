![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2966. [Divide Array Into Arrays With Max Difference](https://leetcode.com/problems/divide-array-into-arrays-with-max-difference)

### Solution :

Method 1 (In weekly contest 376, Loop, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def divideArray(self, nums: List[int], k: int) -> List[List[int]]:
        nums.sort()
        n = len(nums)
        if n % 3 != 0:
            return []

        result = []
        index = 0
        while index+2 < n:
            if nums[index+2] - nums[index] > k:
                return []

            result.append(nums[index:index+3])
            index += 3

        return result
```

Method 2 (Loop, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def divideArray(self, nums: List[int], k: int) -> List[List[int]]:
        result = []
        for num in sorted(nums):
            if len(result) == 0 or len(result[-1]) >= 3:
                result.append([num])
            elif num - result[-1][0] > k:
                return []
            else:
                result[-1].append(num)

        return result
```

Method 3 (Loop, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def divideArray(self, nums: List[int], k: int) -> List[List[int]]:
        nums.sort()
        n = len(nums)
        result = []
        for index in range(0, n, 3):
            if nums[index+2] - nums[index] > k:
                return []

            result.append(nums[index:index+3])

        return result
```
