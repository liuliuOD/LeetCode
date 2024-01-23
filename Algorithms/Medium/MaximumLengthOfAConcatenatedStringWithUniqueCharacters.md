![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
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
