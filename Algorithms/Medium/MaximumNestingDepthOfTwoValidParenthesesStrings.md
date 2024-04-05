![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1111. [Maximum Nesting Depth Of Two Valid Parentheses Strings](https://leetcode.com/problems/maximum-nesting-depth-of-two-valid-parentheses-strings)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maxDepthAfterSplit(self, seq: str) -> List[int]:
        depth, depth_maximum = 0, 0
        for char in seq:
            if char == '(':
                depth += 1
            elif char == ')':
                depth -= 1

            depth_maximum = max(depth_maximum, depth)

        target = depth_maximum // 2
        result = []
        depth, depth_previous = 0, 0
        for char in seq:
            depth_previous = depth
            if char == '(':
                depth += 1
            elif char == ')':
                depth -= 1

            if depth > target or depth_previous > target:
                result.append(1)
            else:
                result.append(0)

        return result
```

Method 2 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maxDepthAfterSplit(self, seq: str) -> List[int]:
        depth, depth_maximum = 0, 0
        for char in seq:
            depth += self.getDepth(char)
            depth_maximum = max(depth_maximum, depth)

        target = depth_maximum // 2
        result = []
        depth, depth_previous = 0, 0
        for char in seq:
            depth_previous = depth
            depth += self.getDepth(char)

            if depth > target or depth_previous > target:
                result.append(1)
            else:
                result.append(0)

        return result

    def getDepth(self, char: str) -> int:
        match char:
            case '(':
                return 1
            case ')':
                return -1
            case _:
                return 0
```
