![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2050. [Parallel Courses III](https://leetcode.com/problems/parallel-courses-iii)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def minimumTime(self, n: int, relations: List[List[int]], time: List[int]) -> int:
        mapping = defaultdict(list)
        for previous, current in relations:
            mapping[current].append(previous)

        memoization = {}
        for index in range(1, n+1):
            self.dfs(index, memoization, mapping, time)

        return max(memoization.values())

    def dfs(self, index: int, memoization, mapping, time):
        if index in memoization:
            return memoization[index]

        result = 0
        for previous in mapping[index]:
            result = max(result, self.dfs(previous, memoization, mapping, time))

        memoization[index] = time[index-1] + result
        return memoization[index]
```

Method 2 (Topological Sort, Time Complexity: $O(M+N)$ (M: amount of `relations`, N: value of `n`)) :
```python
class Solution:
    def minimumTime(self, n: int, relations: List[List[int]], time: List[int]) -> int:
        # Calculate graph && number of relations
        graph = defaultdict(list)
        ingress = [0] * n
        for start, end in relations:
            ingress[end-1] += 1
            graph[start-1].append(end-1)

        # Use BFS to find root && record results
        results = time.copy()
        queue = deque([index for index in range(n) if ingress[index] == 0])
        while queue:
            index_current = queue.popleft()
            for index_next in graph[index_current]:
                results[index_next] = max(results[index_next], time[index_next] + results[index_current])

                ingress[index_next] -= 1
                if ingress[index_next] == 0:
                    queue.append(index_next)

        return max(results)
```
