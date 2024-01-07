![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1235. [Maximum Profit In Job Scheduling](https://leetcode.com/problems/maximum-profit-in-job-scheduling)

### Solution :

Method 1 (DFS + Memoization + Binary Search, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
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

Method 2 (Dynamic Programming + Binary Search, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def jobScheduling(self, start_time: List[int], end_time: List[int], profit: List[int]) -> int:
        n = len(start_time)
        mapping = []
        for index in range(n):
            mapping.append((start_time[index], end_time[index], profit[index]))

        mapping.sort()

        dp = [0] * (n + 1)
        for index in reversed(range(n)):
            index_next = self.binarySearch(index, mapping)
            dp[index] = max(dp[index+1], mapping[index][2] + dp[index_next])

        return dp[0]

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

Method 3 (Dynamic Programming + Binary Search, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def jobScheduling(self, start_time: List[int], end_time: List[int], profit: List[int]) -> int:
        n = len(start_time)
        mapping = []
        for index in range(n):
            mapping.append((start_time[index], index))

        mapping.sort()

        dp = [0] * (n + 1)
        for index in reversed(range(n)):
            index_next = self.binarySearch(index, end_time, mapping)
            dp[index] = max(dp[index+1], profit[mapping[index][1]] + dp[index_next])

        return dp[0]

    def binarySearch(self, index: int, end_time: List[int], mapping: List[Tuple[int, int ,int]]) -> int:
        left = index + 1
        right = len(mapping)
        while left < right:
            middle = left + (right - left) // 2
            if mapping[middle][0] < end_time[mapping[index][1]]:
                left = middle + 1
            else:
                right = middle

        return left
```

Method 4 (Dynamic Programming + Binary Search, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def jobScheduling(self, start_time: List[int], end_time: List[int], profit: List[int]) -> int:
        n = len(start_time)
        mapping = []
        for index in range(n):
            mapping.append((end_time[index], start_time[index], profit[index]))

        mapping.sort()
        dp = [0] * n
        dp[0] = mapping[0][2]
        for index in range(1, n):
            index_previous = self.binarySearch(index, mapping)
            dp[index] = mapping[index][2]
            if index_previous >= 0:
                dp[index] += dp[index_previous]
            dp[index] = max(dp[index], dp[index-1])

        return dp[-1]

    def binarySearch(self, index: int, mapping: List[Tuple[int, int, int]]) -> int:
        left = 0
        right = index - 1
        while left <= right:
            middle = left + (right-left)//2
            # previous end time > current start time
            if mapping[middle][0] > mapping[index][1]:
                right = middle - 1
            else:
                left = middle + 1

        return right
```

Method 5 (Dynamic Programming + Binary Search, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def jobScheduling(self, start_time: List[int], end_time: List[int], profit: List[int]) -> int:
        n = len(start_time)
        mapping = []
        for index in range(n):
            mapping.append((end_time[index], index))

        mapping.sort()
        dp = [0] * n
        dp[0] = profit[mapping[0][1]]
        for index in range(1, n):
            index_previous = self.binarySearch(index, mapping, start_time)
            dp[index] = profit[mapping[index][1]]
            if index_previous >= 0:
                dp[index] += dp[index_previous]
            dp[index] = max(dp[index], dp[index-1])

        return dp[-1]

    def binarySearch(self, index: int, mapping: List[Tuple[int, int, int]], start_time: List[int]) -> int:
        left = 0
        right = index - 1
        while left <= right:
            middle = left + (right-left)//2
            # previous end time > current start time
            if mapping[middle][0] > start_time[mapping[index][1]]:
                right = middle - 1
            else:
                left = middle + 1

        return right
```

### Reference :

- [Intuitions](https://www.techiedelight.com/weighted-interval-scheduling-problem)
