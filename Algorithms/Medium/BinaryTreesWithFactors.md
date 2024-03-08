![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 823. [Binary Trees With Factors](https://leetcode.com/problems/binary-trees-with-factors)

### Solution :

Method 1 (DFS + Memoization) :
```python
MODULO = 1_000_000_007

class Solution:
    def numFactoredBinaryTrees(self, arr: List[int]) -> int:
        existing = set(arr)
        memoization = defaultdict(int)
        for node in arr:
            self.dfs(node, memoization, existing, arr)

        return sum(memoization.values()) % MODULO

    def dfs(self, node_parent, memoization, existing, arr) -> int:
        if node_parent in memoization:
            return memoization[node_parent]

        result = 1
        for node_start in arr:
            if node_parent % node_start != 0:
                continue

            node_next = node_parent // node_start
            if node_next not in existing:
                continue

            """
            why we multiply dfs(left node) by dfs(right node)?
            because the number of combinations in current node is related to its children nodes, and the combinations in the left node can affect the combinations in the right node, and vice versa.
            """
            result = (result + self.dfs(node_start, memoization, existing, arr)*self.dfs(node_next, memoization, existing, arr)) % MODULO

        memoization[node_parent] = result % MODULO
        return memoization[node_parent]
```

Method 2 (DFS + Memoization + Pruning) :
```python
MODULO = 1_000_000_007

class Solution:
    def numFactoredBinaryTrees(self, arr: List[int]) -> int:
        arr.sort()
        existing = set(arr)
        memoization = defaultdict(int)
        for node in arr:
            self.dfs(node, memoization, existing, arr)

        return sum(memoization.values()) % MODULO

    def dfs(self, node_parent, memoization, existing, arr) -> int:
        if node_parent in memoization:
            return memoization[node_parent]

        n = len(arr)
        result = 1
        for node_start in arr:
            if node_start >= node_parent:
                break

            if node_parent % node_start != 0:
                continue

            node_next = node_parent // node_start
            if node_next not in existing:
                continue

            result = (result + self.dfs(node_start, memoization, existing, arr)*self.dfs(node_next, memoization, existing, arr)) % MODULO

        memoization[node_parent] = result % MODULO
        return memoization[node_parent]
```

Method 3 (Dynamic Programming + Pruning) :
```python
MODULO = 1_000_000_007

class Solution:
    def numFactoredBinaryTrees(self, arr: List[int]) -> int:
        arr.sort()

        """
        the following codes will produce wrong answer error because `defaultdict()` will lose those nodes that don't have factors

        dp = defaultdict(lambda: 1)
        """
        dp = {node: 1 for node in arr}
        for node_parent in arr:
            for node_left in arr:
                # factors are always lower than or equal to the square root of the value
                if node_left > node_parent**0.5:
                    break

                node_right = node_parent // node_left
                if node_parent%node_left != 0 or node_right not in dp:
                    continue

                temp = (dp[node_left]*dp[node_right]) % MODULO
                # when the values of the left node and the right node are different, the number of combinations will be twice the original
                if node_left != node_right:
                    temp = (2*temp) % MODULO
                dp[node_parent] = (dp[node_parent] + temp) % MODULO

        return sum(dp.values()) % MODULO
```
