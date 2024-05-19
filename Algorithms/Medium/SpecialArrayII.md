![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3152. [Special Array II](https://leetcode.com/problems/special-array-ii)

### Solution :

Method 1 (In weekly contest 398, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def isArraySpecial(self, nums: List[int], queries: List[List[int]]) -> List[bool]:
        n = len(queries)
        queries_sort = sorted(enumerate(queries), key=lambda query: query[1])
        result = [False] * n
        index_start = 0
        index_end = 0
        is_special = True
        for index, query in queries_sort:
            if query[0] != index_start:
                index_start = index_end = query[0]
                is_special = True

            while index_end < query[1]:
                index_end += 1
                if nums[index_end]%2 == nums[index_end-1]%2:
                    is_special = False
                    break

            result[index] = is_special
        return result
```

Method 2 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def isArraySpecial(self, nums: List[int], queries: List[List[int]]) -> List[bool]:
        n = len(nums)
        prefix_sum = [1]
        for index in range(1, n):
            current = prefix_sum[-1]
            if nums[index]%2 != nums[index-1]%2:
                current += 1
            prefix_sum.append(current)

        result = []
        for index_start, index_end in queries:
            result.append(True if prefix_sum[index_end] - prefix_sum[index_start] == index_end-index_start else False)

        return result
```
