![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2370. [Longest Ideal Subsequence](https://leetcode.com/problems/longest-ideal-subsequence)

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(M*N)$ (M: length of `s`, N: value of `k`), Space Complexity: $O(1)$) :
```python
BASE: int = ord('a')
class Solution:
    def longestIdealString(self, s: str, k: int) -> int:
        dp = [[0]*26 for _ in range(26)]
        for char in s:
            current = ord(char) - BASE
            dp[current][current] = 1 + max(dp[current])
            for offset in range(1, k+1):
                index_previous = current - offset
                if index_previous >= 0:
                    dp[current][index_previous] = 1 + max(dp[index_previous])

                index_next = current + offset
                if index_next < 26:
                    dp[current][index_next] = 1 + max(dp[index_next])

        return max(max(row) for row in dp)
```

Method 2 (Dynamic Programming, Time Complexity: $O(M*N)$ (M: length of `s`, N: value of `k`), Space Complexity: $O(1)$) :
```python
BASE: int = ord('a')
class Solution:
    def longestIdealString(self, s: str, k: int) -> int:
        dp = [[0]*(k*2 + 1) for _ in range(26)]
        for char in s:
            current = ord(char) - BASE
            dp[current][0] = 1 + max(dp[current])
            for offset in range(-k, k+1):
                if offset == 0:
                    continue

                index_previous = current + offset
                if 0 <= index_previous < 26:
                    dp[current][offset] = 1 + max(dp[index_previous])

        return max(max(row) for row in dp)
```
