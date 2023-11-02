![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 501. [Find Mode In Binary Search Tree](https://leetcode.com/problems/find-mode-in-binary-search-tree)

### Follow Up:

- Could you do that without using any extra space? (Assume that the implicit stack space incurred due to recursion does not count).

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Recursive DFS + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        mapping = defaultdict(int)
        self.traverse(root, mapping)

        maximum = max(mapping.values())
        return [key for key, value in mapping.items() if value == maximum]

    def traverse(self, node: Optional[TreeNode], mapping: Dict[int, int]):
        if not node:
            return

        mapping[node.val] += 1
        self.traverse(node.left, mapping)
        self.traverse(node.right, mapping)
```

Method 2 (Iterative DFS + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        maximum = 0
        mapping = defaultdict(int)
        stack = [root]
        while stack:
            node = stack.pop()
            if not node:
                continue

            mapping[node.val] += 1
            maximum = max(maximum, mapping[node.val])
            stack.append(node.right)
            stack.append(node.left)

        return [key for key, value in mapping.items() if value == maximum]
```

Method 3 (BFS + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        maximum = 0
        mapping = defaultdict(int)
        queue = deque([root])
        while queue:
            node = queue.popleft()
            if not node:
                continue

            mapping[node.val] += 1
            maximum = max(maximum, mapping[node.val])
            queue.append(node.left)
            queue.append(node.right)

        return [key for key, value in mapping.items() if value == maximum]
```

Method 4 (In-Order DFS + List, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        """
        Hint: in most cases, a list consumes less memory space and executes faster than a hash map
        """
        nodes_sorted = []
        self.dfs(root, nodes_sorted)

        maximum = 0
        amount_current = 0
        current = nodes_sorted[0]
        result = [nodes_sorted[0]]
        for node in nodes_sorted:
            if node == current:
                amount_current += 1
            else:
                current = node
                amount_current = 1

            if maximum == amount_current:
                result.append(node)
            elif maximum < amount_current:
                maximum = amount_current
                result = [node]

        return result

    def dfs(self, node: Optional[TreeNode], nodes_sorted: List[int]):
        if not node:
            return

        self.dfs(node.left, nodes_sorted)
        nodes_sorted.append(node.val)
        self.dfs(node.right, nodes_sorted)
```

Method 5 (Recursive In-Order DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (if we use the calculation method from the description, then we can say this method has $O(1)$ space complexity)) :
```python
class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        self.current = -inf
        self.amount_current = 0
        self.amount_maximum = 0
        self.result = []

        self.dfs(root)

        return self.result

    def dfs(self, node: Optional[TreeNode]):
        if not node:
            return

        self.dfs(node.left)

        if node.val == self.current:
            self.amount_current += 1
        else:
            self.current = node.val
            self.amount_current = 1

        if self.amount_maximum < self.amount_current:
            self.result = []
            self.amount_maximum = self.amount_current

        if self.amount_maximum == self.amount_current:
            self.result.append(self.current)

        self.dfs(node.right)
```

Method 6 (Iterative In-Order DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        amount_maximum = 0
        amount_current = 0
        current = 0
        result = []

        stack = []
        node = root
        while node or stack:
            while node:
                stack.append(node)
                node = node.left

            node = stack.pop()
            if current == node.val:
                amount_current += 1
            else:
                amount_current = 1
                current = node.val

            if amount_maximum < amount_current:
                result = []
                amount_maximum = amount_current

            if amount_maximum == amount_current:
                result.append(node.val)

            node = node.right

        return result
```

Method 7 (Morris Traversal, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        amount_maximum = 0
        amount_current = 0
        current = 0
        result = []
        node = root
        while node:
            # find `friend node` of current node
            if node.left:
                node_friend = node.left
                while node_friend.right:
                    node_friend = node_friend.right

                node_friend.right = node

                # remove the connection between node and left child
                node_temp = node.left
                node.left = None
                node = node_temp
                continue

            # calculate the result in the in-order traverse
            if current == node.val:
                amount_current += 1
            else:
                amount_current = 1
                current = node.val

            if amount_maximum < amount_current:
                amount_maximum = amount_current
                result = []

            if amount_maximum == amount_current:
                result.append(node.val)

            node = node.right

        return result
```
