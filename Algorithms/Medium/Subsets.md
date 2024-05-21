![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 78. [Subsets](https://leetcode.com/problems/subsets)

### Solution :

Method 1 (Backtracking, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        self.result = []

        self.backtracking(0, [], nums)
        return self.result

    def backtracking(self, index: int, subset: list[int], nums: list[int]):
        if index >= len(nums):
            self.result.append(subset.copy())
            return

        subset.append(nums[index])
        self.backtracking(index+1, subset, nums)
        subset.pop()
        self.backtracking(index+1, subset, nums)
```

Method 2 (Built-In method, Time Complexity: $O(N*2^N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        # Option 1
        result = []
        for amount in range(len(nums)+1):
            result.extend(combinations(nums, amount))

        return result
        """
        # Option 2

        return reduce(lambda result, amount: result + list(combinations(nums, amount)), range(len(nums)+1), [])
        """
```
