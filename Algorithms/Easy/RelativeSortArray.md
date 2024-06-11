![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1122. [Relative Sort Array](https://leetcode.com/problems/relative-sort-array)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M+N*Log(N))$ (M: length of `arr1`, N: length of `arr2`), Space Complexity: $O(M)$) :
```python
class Solution:
    def relativeSortArray(self, arr1: List[int], arr2: List[int]) -> List[int]:
        counter = Counter(arr1)
        result = []
        for num in arr2:
            result.extend([num]*counter[num])
            del counter[num]

        for num in sorted(counter.keys()):
            result.extend([num]*counter[num])

        return result
```

Method 2 (Brute Force, Time Complexity: $O(N+M*Log(M))$ (M: length of `arr1`, N: length of `arr2`), Space Complexity: $O(N)$) :
```python
class Solution:
    def relativeSortArray(self, arr1: List[int], arr2: List[int]) -> List[int]:
        mapping = {num: index for index, num in enumerate(arr2)}
        return sorted(arr1, key=lambda num: (mapping.get(num, inf), num))
```
