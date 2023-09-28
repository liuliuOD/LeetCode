![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 905. [Sort Array By Parity](https://leetcode.com/problems/sort-array-by-parity)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def sortArrayByParity(self, nums: List[int]) -> List[int]:
        pointer = 0
        for index in range(len(nums)):
            if nums[index]%2 == 0:
                nums[index], nums[pointer] = nums[pointer], nums[index]
                pointer += 1
        return nums
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def sortArrayByParity(self, nums: List[int]) -> List[int]:
        even = []
        odd = []
        for num in nums:
            if num%2 == 0:
                even.append(num)
            else:
                odd.append(num)
        return even + odd
```
