![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1751. [Maximum Number Of Events That Can Be Attended II](https://leetcode.com/problems/maximum-number-of-events-that-can-be-attended-ii)

### Solution :

Method 1 (DFS + Dynamic Programming + Memoization) :
```python
class Solution:
    def maxValue(self, events: List[List[int]], k: int) -> int:
        events.sort(key=lambda item: item[0])
        memoization = {}
        return self.dfs(0, events, k, memoization)

    def dfs(self, index: int, events: List[List[int]], k: int, memoization: Dict[str, int]) -> int:
        if index >= len(events) or k <= 0:
            return 0
        
        key_dict = f'{index}-{k}'
        if key_dict in memoization:
            return memoization[key_dict]

        index_next = self.binarySearch(index, events)
        memoization[key_dict] = max(events[index][2] + self.dfs(index_next, events, k-1, memoization), self.dfs(index+1, events, k, memoization))
        return memoization[key_dict]

    def binarySearch(self, index: int, events: List[List[int]]) -> int:
        target = events[index][1]
        pointer_left = index + 1
        pointer_right = len(events)
        while pointer_left < pointer_right:
            middle = pointer_left + (pointer_right - pointer_left) // 2

            if events[middle][0] <= target:
                pointer_left = middle + 1
            else:
                pointer_right = middle
        return pointer_left
```
