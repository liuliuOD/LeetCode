![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 10038. [Maximize The Number Of Partitions After Operations](https://leetcode.com/problems/maximize-the-number-of-partitions-after-operations)

### Solution :

Method 1 (DFS + Memoization) :
```python
BASE = ord('a')
class Solution:
    def maxPartitionsAfterOperations(self, s: str, k: int) -> int:
        s = [ord(char) - BASE for char in s]
        n = len(s)
        memoization = defaultdict(int)

        return 1 + self.dfs(0, 0, True, memoization, s, k)

    def dfs(self, index: int, bitmask: int, can_change: bool, memoization, s, k) -> int:
        n = len(s)
        if index >= n:
            return 0

        key = (index, bitmask, can_change)
        if key in memoization:
            return memoization[key]

        result = self.getOperations(s[index], index, bitmask, can_change, memoization, s, k)
        if can_change:
            for offset in range(26):
                result = max(result, self.getOperations(offset, index, bitmask, not can_change, memoization, s, k))

        memoization[key] = result
        return result

    def getOperations(self, current: int, index: int, bitmask: int, can_change: bool, memoization, s, k) -> int:
        result = 0
        bitmask_current = 1 << current
        bitmask_next = bitmask | bitmask_current
        amount_distinct = bitmask_next.bit_count()
        if amount_distinct > k:
            result = 1 + self.dfs(index+1, bitmask_current, can_change, memoization, s, k)
        else:
            result = self.dfs(index+1, bitmask_next, can_change, memoization, s, k)

        return result
```
