![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
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

Method 2 (Topological Sort variant, Time Complexity: $O(M+N)$ (M: length of `edges`, N: value of `n`)) :
```python
class Solution:
    def findMinHeightTrees(self, n: int, edges: List[List[int]]) -> List[int]:
        graph = [[] for _ in range(n)]
        ingress = [0] * n
        for a, b in edges:
            graph[a].append(b)
            graph[b].append(a)
            ingress[a] += 1
            ingress[b] += 1

        # Option 1
        removal = deque([index for index in range(n) if ingress[index] == 1])
        result = set(range(n))
        while len(result) > 2:
            amount = len(removal)
            for _ in range(amount):
                index = removal.popleft()
                result.remove(index)
                for index_connected in graph[index]:
                    ingress[index_connected] -= 1
                    if ingress[index_connected] == 1:
                        removal.append(index_connected)

        return list(result)
        """
        # Option 2

        result = [index for index in range(n) if ingress[index] in [0, 1]]
        removal = deque(result)
        while removal:
            temp = []
            amount = len(removal)
            for _ in range(amount):
                index = removal.popleft()
                for index_connected in graph[index]:
                    ingress[index_connected] -= 1
                    if ingress[index_connected] == 1:
                        temp.append(index_connected)
                        removal.append(index_connected)

            if len(temp) == 0:
                break
            result = temp

        return result
        """
```
