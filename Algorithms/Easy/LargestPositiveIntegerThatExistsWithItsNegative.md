![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2441. [Largest Positive Integer That Exists With Its Negative](https://leetcode.com/problems/largest-positive-integer-that-exists-with-its-negative)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMaxK(self, nums: List[int]) -> int:
        mapping = set()
        result = -1
        for num in nums:
            mapping.add(num)
            if -num in mapping:
                result = max(result, abs(num))

        return result
```
