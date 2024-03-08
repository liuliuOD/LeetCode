![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1239. [Maximum Length Of A Concatenated String With Unique Characters](https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def maxLength(self, arr: List[str]) -> int:
        memoization = defaultdict(int)
        return self.dfs('', 0, memoization, arr)

    def dfs(self, current: str, index: int, memoization, arr: List[str]) -> int:
        if index >= len(arr):
            return len(current)

        if current in memoization:
            return memoization[current]

        result = self.dfs(current, index+1, memoization, arr)
        if len(set(arr[index])) == len(arr[index]):
            for char in arr[index]:
                if char in current:
                    break
            else:
                result = max(result, self.dfs(current+arr[index], index+1, memoization, arr))

        memoization[current] = result
        return result
```

Method 2 (DFS + Memoization + Bitmask) :
```python
BASE: int = ord('a')
class Solution:
    def maxLength(self, arr: List[str]) -> int:
        memoization: Dict[int, int] = defaultdict(int)
        return self.dfs(0, 0, memoization, arr)

    def dfs(self, bitmask: int, index: int, memoization: Dict[int, int], arr: List[str]) -> int:
        if index >= len(arr):
            return bin(bitmask).count('1')

        if bitmask in memoization:
            return memoization[bitmask]

        result = self.dfs(bitmask, index+1, memoization, arr)
        if len(set(arr[index])) == len(arr[index]):
            # Option 1
            for char in arr[index]:
                if (1 << (ord(char) - BASE)) & bitmask:
                    break
            else:
                result = max(result, self.dfs(reduce(lambda a, b: a | (1 << (ord(b) - BASE)), arr[index], bitmask), index+1, memoization, arr))
            """
            # Option 2

            bitmask_temp = bitmask
            for char in arr[index]:
                current = 1 << (ord(char) - BASE)
                if current & bitmask:
                    break

                bitmask_temp |= current
            else:
                result = max(result, self.dfs(bitmask_temp, index+1, memoization, arr))
            """

        memoization[bitmask] = result
        return result
```
