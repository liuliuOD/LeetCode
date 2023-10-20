![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 565. [Array Nesting](https://leetcode.com/problems/array-nesting)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded", 858/885) :
```python
class Solution:
    def arrayNesting(self, nums: List[int]) -> int:
        result = 0
        for index, num in enumerate(nums):
            result = max(result, self.dfs(index, set(), nums))

        return result

    def dfs(self, index: int, visited: Set[int], nums: List[int]) -> int:
        if nums[index] in visited:
            return 0
        visited.add(nums[index])

        return 1 + self.dfs(nums[index], visited, nums)
```

Method 2 (DFS) :
```python
class Solution:
    def arrayNesting(self, nums: List[int]) -> int:
        result = 0
        visited = set()
        for index, num in enumerate(nums):
            result = max(result, self.dfs(index, visited, nums))

        return result

    def dfs(self, index: int, visited: Set[int], nums: List[int]) -> int:
        if nums[index] in visited:
            return 0
        visited.add(nums[index])

        return 1 + self.dfs(nums[index], visited, nums)
```

Method 3 (Time Complexity: $O(N)$) :
```python
class Solution:
    def arrayNesting(self, nums: List[int]) -> int:
        visited = set()
        result = 0
        for num in nums:
            if num in visited:
                continue
            visited.add(num)

            temp = 1
            while nums[num] not in visited:
                visited.add(nums[num])
                num = nums[num]
                temp += 1

            result = max(result, temp)

        return result
```

Method 4 (Union Find) :
```python
class UnionFind:
    def __init__(self, n: int):
        self.items = list(range(n))
        self.lengths = [1] * n

    def find(self, value: int) -> int:
        if self.items[value] != value:
            self.items[value] = self.find(self.items[value])

        return self.items[value]

    def union(self, a: int, b: int):
        parent_a = self.find(a)
        parent_b = self.find(b)
        if parent_a == parent_b:
            return

        self.items[parent_a] = parent_b
        """
        # Crucial code

        Wrong answer when change to `self.lengths[parent_a] += self.lengths[parent_b]`
        """
        self.lengths[parent_b] += self.lengths[parent_a]

class Solution:
    def arrayNesting(self, nums: List[int]) -> int:
        union_find = UnionFind(len(nums))
        for index, num in enumerate(nums):
            union_find.union(index, num)

        return max(union_find.lengths)
```
