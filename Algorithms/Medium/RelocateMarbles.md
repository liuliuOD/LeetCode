![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2766. [Relocate Marbles](https://leetcode.com/problems/relocate-marbles)

### Solution :

Method 1 (Set) :
```python
class Solution:
    def relocateMarbles(self, nums: List[int], moveFrom: List[int], moveTo: List[int]) -> List[int]:
        mapping = set()
        for num in nums:
            mapping.add(num)

        for move_f, move_t in zip(moveFrom, moveTo):
            if move_f in mapping and move_f != move_t:
                mapping.remove(move_f)
                mapping.add(move_t)

        return sorted(list(mapping))
```

Method 2 (Set) :
```python
class Solution:
    def relocateMarbles(self, nums: List[int], moveFrom: List[int], moveTo: List[int]) -> List[int]:
        result = set(nums)
        for move_f, move_t in zip(moveFrom, moveTo):
            if move_f in result and move_f != move_t:
                result.remove(move_f)
                result.add(move_t)

        return sorted(result)
```
