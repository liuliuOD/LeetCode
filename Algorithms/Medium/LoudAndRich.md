![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 851. [Loud And Rich](https://leetcode.com/problems/loud-and-rich)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def loudAndRich(self, richer: List[List[int]], quiet: List[int]) -> List[int]:
        # build graph from less rich to more rich
        graph = defaultdict(list)
        for more, less in richer:
            graph[less].append(more)

        n = len(quiet)
        memoization = [None] * n
        for index in range(n):
            self.dfs(index, memoization, graph, quiet)

        return [index for _, index in memoization]

    def dfs(self, index: int, memoization, graph: Dict[int, List[int]], quiet: List[int]) -> int:
        if memoization[index] is not None:
            return memoization[index]

        result = (quiet[index], index)
        for index_more in graph[index]:
            more = self.dfs(index_more, memoization, graph, quiet)
            if more[0] < result[0]:
                result = more

        memoization[index] = result
        return result
```

Method 2 (Topological Sort) :
```python
class Solution:
    def loudAndRich(self, richer: List[List[int]], quiet: List[int]) -> List[int]:
        n = len(quiet)
        # build graph from more rich to less rich
        graph = defaultdict(list)
        ingress = [0] * n
        for more, less in richer:
            graph[more].append(less)
            ingress[less] += 1

        # by default, each node is set to itself
        result = list(range(n))
        queue = deque([index for index in range(n) if ingress[index] == 0])
        while queue:
            index = queue.popleft()
            for index_less in graph[index]:
                # Compare the current node to the next node, and if the `quiet` value in the result of the current node is less than the `quiet` value in the result of the next node, set the result in the next node to the current node
                if quiet[result[index_less]] > quiet[result[index]]:
                    result[index_less] = result[index]

                ingress[index_less] -= 1
                if ingress[index_less] == 0:
                    queue.append(index_less)

        return result
```
