![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2149. [Rearrange Array Elements By Sign](https://leetcode.com/problems/rearrange-array-elements-by-sign)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def rearrangeArray(self, nums: List[int]) -> List[int]:
        positive = []
        negative = []
        for num in nums:
            if num < 0:
                negative.append(num)
            else:
                positive.append(num)

        result = []
        while positive or negative:
            if positive:
                result.append(positive.pop(0))
            if negative:
                result.append(negative.pop(0))

        return result
```

Method 2 (Reverse Order, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def rearrangeArray(self, nums: List[int]) -> List[int]:
        positive = []
        negative = []
        for num in reversed(nums):
            if num < 0:
                negative.append(num)
            else:
                positive.append(num)

        result = []
        while positive or negative:
            if positive:
                result.append(positive.pop())
            if negative:
                result.append(negative.pop())

        return result
```

Method 3 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def rearrangeArray(self, nums: List[int]) -> List[int]:
        n = len(nums)
        result = []
        index_positive = 0
        index_negative = 0
        while index_positive < n or index_positive < n:
            while (not result or result[-1] < 0) and index_positive < n:
                if nums[index_positive] >= 0:
                    result.append(nums[index_positive])

                index_positive += 1

            while result[-1] >= 0 and index_negative < n:
                if nums[index_negative] < 0:
                    result.append(nums[index_negative])

                index_negative += 1

        return result
```

Method 4 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def rearrangeArray(self, nums: List[int]) -> List[int]:
        n = len(nums)
        result = [0] * n
        index_positive = 0
        index_negative = 1
        for num in nums:
            if num >= 0:
                result[index_positive] = num
                index_positive += 2
            else:
                result[index_negative] = num
                index_negative += 2

        return result
```
