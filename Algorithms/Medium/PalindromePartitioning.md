![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 131. [Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning)

### Solution :

Method 1 (Backtracking + Two Pointer) :
```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        self.result = []
        self.backtracking(0, [], "", s)

        return self.result

    def backtracking(self, index: int, substrings: list[str], substring: str, s: str):
        if index >= len(s):
            if self.is_palindrome(substring):
                temp = substrings.copy()
                temp.append(substring)
                self.result.append(temp)
            return

        self.backtracking(index+1, substrings, substring+s[index], s)
        if self.is_palindrome(substring):
            substrings.append(substring)
            self.backtracking(index+1, substrings, s[index], s)
            substrings.pop()

    def is_palindrome(self, s: str) -> bool:
        n = len(s)
        if n == 0:
            return False

        left = 0
        right = n - 1
        while left < right:
            if s[left] != s[right]:
                return False

            left += 1
            right -= 1

        return True
```

Method 2 (Backtracking + Two Pointer + Memoization) :
```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        n = len(s)
        memoization: list[list[int]] = [[-1] * n for _ in range(n)]
        result = []
        self.backtracking(0, memoization, result, [], s)
        return result

    def backtracking(self, index_start: int, memoization: list[list[int]], result: list[list[str]], subset: list[str], s: str):
        n = len(s)
        if index_start >= n:
            result.append(subset.copy())
            return

        for index_end in range(index_start, n):
            if not self.is_palindrome(index_start, index_end, memoization, s):
                continue

            subset.append(s[index_start:index_end+1])
            self.backtracking(index_end+1, memoization, result, subset, s)
            subset.pop()

    def is_palindrome(self, left: int, right: int, memoization: list[list[int]], s: str) -> bool:
        if memoization[left][right] != -1:
            return bool(memoization[left][right])

        while left < right:
            if s[left] != s[right]:
                memoization[left][right] = int(False)
                return False

            left += 1
            right -= 1

        memoization[left][right] = int(True)
        return True
```

Method 3 (Backtracking + Two Pointer + Built-In Method) :
```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        n = len(s)
        result = []
        self.backtracking(0, result, [], s)
        return result

    def backtracking(self, index_start: int, result: list[list[str]], subset: list[str], s: str):
        n = len(s)
        if index_start >= n:
            result.append(subset.copy())
            return

        for index_end in range(index_start, n):
            if not self.is_palindrome(index_start, index_end, s):
                continue

            subset.append(s[index_start:index_end+1])
            self.backtracking(index_end+1, result, subset, s)
            subset.pop()

    @cache
    def is_palindrome(self, left: int, right: int, s: str) -> bool:
        while left < right:
            if s[left] != s[right]:
                return False

            left += 1
            right -= 1

        return True
```
