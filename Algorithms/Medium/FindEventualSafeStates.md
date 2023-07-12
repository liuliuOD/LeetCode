![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 802. [Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states)

### Solution :

Method 1 (DFS + Backtracking, ERROR: "Time Limit Exceeded", 93/112) :
```python
class Solution:
    def eventualSafeNodes(self, graph: List[List[int]]) -> List[int]:
        result = []
        self.graph = graph
        for index in range(len(graph)):
            traversed_nodes = set()
            if self.isNormalNode(index, traversed_nodes):
                continue

            result.append(index)
        return result
    
    def isNormalNode(self, index: int, traversed_nodes: List[int]) -> bool:
        if index in traversed_nodes:
            traversed_nodes.remove(index)
            return True
        traversed_nodes.add(index)
        
        for index_next in self.graph[index]:
            if not self.isNormalNode(index_next, traversed_nodes):
                continue
            return True
        
        traversed_nodes.remove(index)
        return False
```

Method 2 (Want to reduce Space Usage, ERROR: "Time Limit Exceeded", 112/112) :
```python
class Solution:
    def eventualSafeNodes(self, graph: List[List[int]]) -> List[int]:
        memoization = {}
        for index in range(len(graph)):
            self.graph = graph.copy()
            traversed_nodes = set()
            self.classifyNode(index, traversed_nodes, memoization)
        return sorted(dict(filter(lambda item: item[1] == False, memoization.items())).keys())

    def classifyNode(self, index: int, traversed_nodes: List[int], memoization: List[int]) -> bool:
        if index in memoization:
            return memoization[index]

        if index in traversed_nodes:
            memoization[index] = True
            traversed_nodes.remove(index)
            return memoization[index]
        traversed_nodes.add(index)

        for index_next in self.graph[index]:
            if not self.classifyNode(index_next, traversed_nodes, memoization):
                continue
            return True

        traversed_nodes.remove(index)
        memoization[index] = False
        return memoization[index]
```

Method 3-1 (DFS + Backtracking + Memoization) :
```python
class Solution:
    def eventualSafeNodes(self, graph: List[List[int]]) -> List[int]:
        result = []
        # record traversed nodes are normal or not
        memoization = {}
        self.graph = graph
        for index in range(len(graph)):
            traversed_nodes = set()
            if self.isNormalNode(index, traversed_nodes, memoization):
                continue

            result.append(index)
        return result

    def isNormalNode(self, index: int, traversed_nodes: List[int], memoization: List[int]) -> bool:
        if index in memoization:
            return memoization[index]

        if index in traversed_nodes:
            memoization[index] = True
            traversed_nodes.remove(index)
            return memoization[index]
        traversed_nodes.add(index)

        for index_next in self.graph[index]:
            if not self.isNormalNode(index_next, traversed_nodes, memoization):
                continue
            memoization[index] = True
            return memoization[index]

        traversed_nodes.remove(index)
        memoization[index] = False
        return memoization[index]
```

Method 3-2 (Refactor) :
```python
class Solution:
    def eventualSafeNodes(self, graph: List[List[int]]) -> List[int]:
        result = []
        # record traversed nodes are normal or not
        memoization = {}
        self.graph = graph
        for index in range(len(graph)):
            traversed_nodes = set()
            if self.isNormalNode(index, traversed_nodes, memoization):
                continue

            result.append(index)
        return result

    def isNormalNode(self, index: int, traversed_nodes: List[int], memoization: List[int]) -> bool:
        if index in traversed_nodes:
            memoization[index] = True
            traversed_nodes.remove(index)

        if index in memoization:
            return memoization[index]

        traversed_nodes.add(index)

        for index_next in self.graph[index]:
            if self.isNormalNode(index_next, traversed_nodes, memoization):
                memoization[index] = True
                return memoization[index]

        traversed_nodes.remove(index)
        memoization[index] = False
        return memoization[index]
```

Method 4-1 (DFS + Memoization) :
```python
class Solution:
    def eventualSafeNodes(self, graph: List[List[int]]) -> List[int]:
        result = []
        # record traversed nodes are normal or not
        memoization = {}
        self.graph = graph
        for index in range(len(graph)):
            traversed_nodes = set()
            if self.isNormalNode(index, traversed_nodes, memoization):
                continue

            result.append(index)
        return result

    def isNormalNode(self, index: int, traversed_nodes: List[int], memoization: List[int]) -> bool:
        if index in memoization:
            return memoization[index]

        if index in traversed_nodes:
            return True
        traversed_nodes.add(index)

        for index_next in self.graph[index]:
            if self.isNormalNode(index_next, traversed_nodes, memoization):
                memoization[index] = True
                return memoization[index]

        memoization[index] = False
        return memoization[index]
```

Method 4-2 (Want to reduce Space Usage) :
```python
class Solution:
    def eventualSafeNodes(self, graph: List[List[int]]) -> List[int]:
        # record traversed nodes are normal or not
        memoization = {}
        self.graph = graph
        for index in range(len(graph)):
            traversed_nodes = set()
            self.classifyNode(index, traversed_nodes, memoization)

        return sorted(dict(filter(lambda pair: pair[1] is False, memoization.items())))

    def classifyNode(self, index: int, traversed_nodes: List[int], memoization: List[int]) -> bool:
        if index in memoization:
            return memoization[index]

        if index in traversed_nodes:
            return True
        traversed_nodes.add(index)

        for index_next in self.graph[index]:
            if self.classifyNode(index_next, traversed_nodes, memoization):
                memoization[index] = True
                return memoization[index]

        memoization[index] = False
        return memoization[index]
```
