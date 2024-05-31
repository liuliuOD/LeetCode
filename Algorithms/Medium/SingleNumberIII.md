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

Method 2 (XOR, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> List[int]:
        xor_all = reduce(lambda a, b: a^b, nums)
        position = 0
        while xor_all & (1 << position) == 0:
            position += 1

        xor_group_0, xor_group_1 = 0, 0
        for num in nums:
            if num & (1 << position) == 0:
                xor_group_0 ^= num
            else:
                xor_group_1 ^= num

        return [xor_group_0, xor_group_1]
```
