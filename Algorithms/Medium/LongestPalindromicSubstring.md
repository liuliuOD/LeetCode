![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 5. [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded", 142/142) :
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)

        result = ''
        for index_start in range(n):
            for index_end in reversed(range(index_start, n)):
                if self.isPalindrome(index_start, index_end, s):
                    if len(result) < (index_end-index_start+1):
                        result = s[index_start:index_end+1]

                    break

        return result

    def isPalindrome(self, left, right, s) -> bool:
        if left > right or s[left] != s[right]:
            return False

        if left == right or (left+1 == right and s[left] == s[right]):
            return True

        return self.isPalindrome(left+1, right-1, s)
```

Method 2 (DFS, Cost Runtime: 9929 ms, Cost Memory: 24.2 MB) :
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

Method 3 (DFS + Memoization (by Dictionary), Cost Runtime: 6851 ms, Cost Memory: 80.9 MB) :
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)

        memoization = {}
        result = ''
        for index_start in range(n):
            for index_end in reversed(range(index_start, n)):
                if self.isPalindrome(index_start, index_end, memoization, s):
                    if len(result) < (index_end-index_start+1):
                        result = s[index_start:index_end+1]

                    break

        return result

    def isPalindrome(self, left: int, right: int, memoization: Dict[str, bool], s: str) -> bool:
        key = f'{left}-{right}'
        if key in memoization:
            return memoization[key]

        if left > right or s[left] != s[right]:
            return False

        if left == right or (left+1 == right and s[left] == s[right]):
            return True

        memoization[key] = self.isPalindrome(left+1, right-1, memoization, s)
        return memoization[key]
```

Method 4 (DFS + Memoization (by List), Cost Runtime: 3838 ms, Cost Memory: 24.7 MB) :
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)

        memoization = [[None]*n for _ in range(n)]
        result = ''
        for index_start in range(n):
            for index_end in reversed(range(index_start, n)):
                if self.isPalindrome(index_start, index_end, memoization, s):
                    if len(result) < (index_end-index_start+1):
                        result = s[index_start:index_end+1]

                    break

        return result

    def isPalindrome(self, left: int, right: int, memoization: List[List[bool]], s: str) -> bool:
        if memoization[left][right] is not None:
            return memoization[left][right]

        if left > right or s[left] != s[right]:
            return False

        if left == right or (left+1 == right and s[left] == s[right]):
            return True

        memoization[left][right] = self.isPalindrome(left+1, right-1, memoization, s)
        return memoization[left][right]
```

Method 5 (From Center to 2 sides) :
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
