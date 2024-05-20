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
