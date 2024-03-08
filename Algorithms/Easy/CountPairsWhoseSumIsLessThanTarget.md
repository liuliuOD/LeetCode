![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2824. [Count Pairs Whose Sum Is Less Than Target](https://leetcode.com/problems/count-pairs-whose-sum-is-less-than-target)

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def countPairs(self, nums: List[int], target: int) -> int:
        n = len(nums)
        result = 0
        for i in range(n):
            for j in range(i+1, n):
                if nums[i] + nums[j] < target:
                    result += 1

        return result
```

Method 2 (Two Pointer) :
```python
class Solution:
    def countPairs(self, nums: List[int], target: int) -> int:
        result = 0
        left = 0
        right = len(nums) - 1
        nums.sort()

        while left < right:
            if nums[left] + nums[right] >= target:
                right -= 1
                continue

            result += right - left
            left += 1

        return result
```
