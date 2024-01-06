![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1235. [Maximum Profit In Job Scheduling](https://leetcode.com/problems/maximum-profit-in-job-scheduling)

### Solution :

Method 1 (DFS + Memoization + Binary Search) :
```python
class Solution:
    def jobScheduling(self, start_time: List[int], end_time: List[int], profit: List[int]) -> int:
        n = len(start_time)
        mapping = []
        for index in range(n):
            mapping.append((start_time[index], end_time[index], profit[index]))

        mapping.sort()

        memoization = defaultdict(int)
        return self.dfs(0, memoization, mapping)

    def dfs(self, index: int, memoization: Dict[Tuple[int, int], int], mapping: List[Tuple[int, int, int]]) -> int:
        if index >= len(mapping):
            return 0

        key = index
        if key in memoization:
            return memoization[key]

        index_next = self.binarySearch(index, mapping)
        _, _, profit = mapping[index]
        result = max(self.dfs(index+1, memoization, mapping), profit + self.dfs(index_next, memoization, mapping))

        memoization[key] = result
        return result

    def binarySearch(self, index: int, mapping: List[Tuple[int, int ,int]]) -> int:
        left = index + 1
        right = len(mapping)
        while left < right:
            middle = left + (right - left) // 2
            if mapping[middle][0] < mapping[index][1]:
                left = middle + 1
            else:
                right = middle

        return left
```
