![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 260. [Single Number III](https://leetcode.com/problems/single-number-iii)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> List[int]:
        result: set[int] = set()
        for num in nums:
            if num in result:
                result.remove(num)
            else:
                result.add(num)

        return list(result)
```
