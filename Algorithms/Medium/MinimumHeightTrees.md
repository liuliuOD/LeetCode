![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 310. [Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees)

### Solution :

Method 1 (Topological Sort variant, Time Complexity: $O(M+N)$ (M: length of `edges`, N: value of `n`)) :
```python
class Solution:
    def findMinHeightTrees(self, n: int, edges: List[List[int]]) -> List[int]:
        if n == 1:
            return [0]

        graph = defaultdict(list)
        ingress = [0] * n
        for start, end in edges:
            graph[start].append(end)
            graph[end].append(start)
            ingress[start] += 1
            ingress[end] += 1

        queue = deque()
        for index in range(n):
            """
            there is exactly 1 edge between 2 nodes, so we can say the node is leaf if ingress[index] is 1

            To prevent duplicate calculations, need to substract 1 from `ingress[index]`
            """
            if ingress[index] == 1:
                queue.append(index)
                ingress[index] -= 1

        result = []
        while queue:
            result = []
            amount = len(queue)
            for _ in range(amount):
                index = queue.popleft()
                result.append(index)
                for index_next in graph[index]:
                    ingress[index_next] -= 1
                    if ingress[index_next] == 1:
                        queue.append(index_next)

        return result
```
