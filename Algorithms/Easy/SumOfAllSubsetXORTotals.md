![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1863. [Sum Of All Subset XOR Totals](https://leetcode.com/problems/sum-of-all-subset-xor-totals)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N*2^N)$, Space Complexity: $O(2^N)$) :
```python
class Solution:
    def subsetXORSum(self, nums: List[int]) -> int:
        n = len(nums)
        result = 0
        for digit in range(1, n+1):
            for subset in combinations(nums, digit):
                result += reduce(lambda a, b: a^b, subset)

        return result
```

Method 2 (Backtracking, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def subsetXORSum(self, nums: List[int]) -> int:
        return self.backtracking(0, 0, nums)

    def backtracking(self, index: int, current: int, nums: list[int]) -> int:
        if index >= len(nums):
            return current

        return self.backtracking(index+1, current^nums[index], nums) + self.backtracking(index+1, current, nums)
```
