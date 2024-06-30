![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1579. [Remove Max Number Of Edges To Keep Graph Fully Traversable](https://leetcode.com/problems/remove-max-number-of-edges-to-keep-graph-fully-traversable)

### Solution :

Method 1 (Union Find, Time Complexity: $O(M+N)$ (M: number of the elements in `edges`, N: value of `n`), Space Complexity: $O(N)$) :
```python
class UnionFind:
    def __init__(self, n: int):
        self.root = list(range(n))
        self.unconnected_nodes = n - 1

    def find(self, num: int) -> int:
        if num != self.root[num]:
            self.root[num] = self.find(self.root[num])
        return self.root[num]

    def union(self, a: int, b: int) -> bool:
        root_a = self.find(a)
        root_b = self.find(b)

        if root_a == root_b:
            return False

        self.root[root_a] = root_b
        self.unconnected_nodes -= 1
        return True

    def get_unconnected_amount(self) -> int:
        return self.unconnected_nodes

class Solution:
    def maxNumEdgesToRemove(self, n: int, edges: List[List[int]]) -> int:
        union_find_alice = UnionFind(n)
        union_find_bob = UnionFind(n)

        amount_connected = 0
        for t, u, v in edges:
            if t != 3:
                continue

            is_connected = union_find_alice.union(u-1, v-1)
            is_connected |= union_find_bob.union(u-1, v-1)
            if is_connected:
                amount_connected += 1

        for t, u, v in edges:
            is_connected = False
            if t == 1:
                is_connected = union_find_alice.union(u-1, v-1)
            elif t == 2:
                is_connected = union_find_bob.union(u-1, v-1)

            if is_connected:
                amount_connected += 1

        if union_find_alice.get_unconnected_amount() or union_find_bob.get_unconnected_amount():
            return -1

        return len(edges) - amount_connected
```
