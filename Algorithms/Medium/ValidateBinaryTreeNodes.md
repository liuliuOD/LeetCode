![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1361. [Validate Binary Tree Nodes](https://leetcode.com/problems/validate-binary-tree-nodes)

### Solution :

Method 1 (Union Find) :
```python
class UnionFind:
    def __init__(self, n: int):
        self.items = list(range(n))
        self.amount_group = n

    def find(self, i: int) -> int:
        if self.items[i] != i:
            self.items[i] = self.find(self.items[i])
        return self.items[i]

    def union(self, i: int, j: int):
        root_i, root_j = self.find(i), self.find(j)
        if root_i == root_j:
            return

        self.items[root_i] = root_j
        self.amount_group -= 1

class Solution:
    def validateBinaryTreeNodes(self, n: int, left_child: List[int], right_child: List[int]) -> bool:
        """
        1. only exists 1 root
        2. doesn't have cycle
        3. each node need to exist exactly 1 ingress, and has at most 2 outgress
        """
        union_find = UnionFind(n)
        parents = [0] * n
        for index in range(n):
            if left_child[index] != -1:
                union_find.union(index, left_child[index])
                parents[left_child[index]] += 1
            if right_child[index] != -1:
                union_find.union(index, right_child[index])
                parents[right_child[index]] += 1

        counter = Counter(parents)
        return union_find.amount_group == 1 and counter[0] == 1 and counter[1] == n-1
```

Method 2 (BFS + Adjacency List) :
```python
class Solution:
    def validateBinaryTreeNodes(self, n: int, left_child: List[int], right_child: List[int]) -> bool:
        ingress = [0] * n
        graph = defaultdict(list)
        for index in range(n):
            if left_child[index] != -1:
                left = left_child[index]
                ingress[left] += 1
                graph[index].append(left)
            if right_child[index] != -1:
                right = right_child[index]
                ingress[right] += 1
                graph[index].append(right)

        root = [index for index in range(n) if ingress[index] == 0]
        if len(root) != 1:
            return False
        root = root[0]

        visited = set([root])
        queue = deque([root])
        while queue:
            node = queue.popleft()
            for children in graph[node]:
                # each node has at most 1 ingress
                if children in visited:
                    return False
                visited.add(children)

                queue.append(children)

        # each node has been visited exactly once
        return len(visited) == n
```

Method 3 (BFS) :
```python
class Solution:
    def validateBinaryTreeNodes(self, n: int, left_child: List[int], right_child: List[int]) -> bool:
        ingress = [0] * n
        for index in range(n):
            if left_child[index] != -1:
                ingress[left_child[index]] += 1
            if right_child[index] != -1:
                ingress[right_child[index]] += 1

        root = [index for index in range(n) if ingress[index] == 0]
        if len(root) != 1:
            return False
        root = root[0]

        visited = set()
        queue = deque([root])
        while queue:
            index = queue.popleft()
            if index in visited:
                return False
            visited.add(index)

            if left_child[index] != -1:
                queue.append(left_child[index])
            if right_child[index] != -1:
                queue.append(right_child[index])

        return len(visited) == n
```
