![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 5. [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring)

### Solution :

Method 1 (Dynamic Programming, execute almost 10s) :
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        self.s = s
        self.memoization = [[False]*n for _ in range(n)]
        index_maximum_start = 0
        index_maximum_end = 0
        for offset in range(n):
            for pointer_left in range(0, n-offset):
                pointer_right = pointer_left + offset
                if not self.isPalindrome(pointer_left, pointer_right) or offset < (index_maximum_end - index_maximum_start + 1):
                    continue

                index_maximum_start = pointer_left
                index_maximum_end = pointer_right

        return s[index_maximum_start:index_maximum_end+1]
    
    def isPalindrome(self, pointer_left: int, pointer_right: int) -> bool:
        if pointer_left == pointer_right:
            self.memoization[pointer_left][pointer_right] = True
        elif (pointer_right - pointer_left) == 1:
            self.memoization[pointer_left][pointer_right] = (self.s[pointer_left] == self.s[pointer_right])
        elif self.s[pointer_left] == self.s[pointer_right]:
            self.memoization[pointer_left][pointer_right] = self.memoization[pointer_left+1][pointer_right-1]
        else:
            self.memoization[pointer_left][pointer_right] = False

        return self.memoization[pointer_left][pointer_right]
```

Method 2 (From Center to 2 sides) :
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        self.s = s
        self.result_start = 0
        self.result_end = 0
        for index_s in range(len(s)):
            # for 1 center: aba
            self.findPalindrome(index_s, index_s)
            # for 2 center: abba
            self.findPalindrome(index_s, index_s+1)

        return s[self.result_start:self.result_end+1]
    
    def findPalindrome(self, pointer_left: int, pointer_right: int):
        while pointer_left >= 0 and pointer_right < len(self.s) and self.s[pointer_left] == self.s[pointer_right]:
            pointer_left -= 1
            pointer_right += 1
        
        if (pointer_right - pointer_left - 1) > (self.result_end - self.result_start + 1):
            self.result_start = pointer_left + 1
            self.result_end = pointer_right - 1
```
