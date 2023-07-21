![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 45. [Jump Game II](https://leetcode.com/problems/jump-game-ii)

### Solution :

Method 1 (DP, ERROR: "Time Limit Exceeded", 73/109) :
```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        n = len(nums)
        memoization = [float('inf')] * n

        self.dfs(0, 0, memoization, nums)
        return memoization[n-1]
    
    def dfs(self, index: int, jumps: int, memoization: List[int], nums: List[int]):
        n = len(nums)
        if index == n-1:
            memoization[index] = min(memoization[index], jumps)
            return None
        
        if index in memoization and memoization[index] < jumps:
            return None

        memoization[index] = jumps

        for index_next in range(index+1, min(index+nums[index]+1, n)):
            self.dfs(index_next, jumps+1, memoization, nums)
```

Method 2 (BFS, ERROR: "Time Limit Exceeded", 82/109) :
```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        return self.bfs(nums)

    def bfs(self, nums: List[int]) -> int:
        n = len(nums)
        memoization = [float('inf')] * n

        queue = deque([(0, 0)])
        while queue:
            index_current, jump_current = queue.popleft()
            if index_current == n-1:
                return jump_current

            if index_current in memoization and memoization[index_current] < jump_current:
                continue
            memoization[index_current] = jump_current

            for index_next in range(index_current+1, min(n, index_current+nums[index_current]+1)):
                jump_next = jump_current + 1
                if index_next in memoization and memoization[index_next] < jump_next:
                    continue
                queue.append((index_next, jump_next))

        return -1
```

Method 3 (Two Pointer) :
```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        return self.bfs(nums)

    def bfs(self, nums: List[int]) -> int:
        n = len(nums)
        jumps = 0
        pointer_left = 0
        pointer_right = 1
        while pointer_left < pointer_right and pointer_right < n:
            temp = pointer_right
            for index in range(pointer_left, pointer_right):
                temp = max(temp, index+nums[index])
            jumps += 1
            pointer_left = pointer_right
            pointer_right = temp + 1
        
        return jumps
```
