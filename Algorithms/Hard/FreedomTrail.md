![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 514. [Freedom Trail](https://leetcode.com/problems/freedom-trail)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(M*N)$ (M: length of `ring`, N: length of `key`), Space Complexity: $O(M*N)$) :
```python
class Solution:
    def findRotateSteps(self, ring: str, key: str) -> int:
        return min(self.dfs(0, 0, 1, ring, key), self.dfs(0, 0, -1, ring, key))

    @cache
    def dfs(self, index_ring: int, index_key: int, direction: int, ring: str, key: str) -> int:
        n_ring = len(ring)
        if index_ring < 0:
            index_ring = n_ring - 1
        elif index_ring >= n_ring:
            index_ring = 0

        if index_key >= len(key):
            return 0

        result = inf
        if ring[index_ring] == key[index_key]:
            result = min(result, 1 + self.dfs(index_ring, index_key+1, direction, ring, key), 1 + self.dfs(index_ring, index_key+1, -direction, ring, key))
        else:
            result = min(result, 1 + self.dfs(index_ring+direction, index_key, direction, ring, key))

        return result
```

Method 2 (DFS + Memoization, Time Complexity: $O(M*N)$ (M: length of `ring`, N: length of `key`), Space Complexity: $O(M*N)$) :
```python
class Solution:
    def findRotateSteps(self, ring: str, key: str) -> int:
        n_ring = len(ring)

        @cache
        def dfs(index_ring: int, index_key: int, direction: int) -> int:
            if index_ring < 0:
                index_ring = n_ring - 1
            elif index_ring >= n_ring:
                index_ring = 0

            if index_key >= len(key):
                return 0

            result = inf
            if ring[index_ring] == key[index_key]:
                result = min(result, 1 + dfs(index_ring, index_key+1, direction), 1 + dfs(index_ring, index_key+1, -direction))
            else:
                result = min(result, 1 + dfs(index_ring+direction, index_key, direction))

            return result

        return min(dfs(0, 0, 1), dfs(0, 0, -1))
```

Method 3 (DFS + Memoization, Time Complexity: $O(M*N)$ (M: length of `ring`, N: length of `key`), Space Complexity: $O(M*N)$) :
```python
class Solution:
    def findRotateSteps(self, ring: str, key: str) -> int:
        n_ring = len(ring)

        memoization = {}
        def dfs(index_ring: int, index_key: int, direction: int) -> int:
            key_m = (index_ring, index_key, direction)
            if key_m in memoization:
                return memoization[key_m]

            if index_ring < 0:
                index_ring = n_ring - 1
            elif index_ring >= n_ring:
                index_ring = 0

            if index_key >= len(key):
                return 0

            result = inf
            if ring[index_ring] == key[index_key]:
                result = min(result, 1 + dfs(index_ring, index_key+1, direction), 1 + dfs(index_ring, index_key+1, -direction))
            else:
                result = min(result, 1 + dfs(index_ring+direction, index_key, direction))

            memoization[key_m] = result
            return result

        return min(dfs(0, 0, 1), dfs(0, 0, -1))
```
