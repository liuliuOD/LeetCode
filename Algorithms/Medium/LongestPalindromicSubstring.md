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

Method 2 (DFS + Pruning, Cost Runtime: 9929 ms, Cost Memory: 24.2 MB) :
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

Method 3 (Two Pointers + Pruning, Time Complexity: $O(N^3)$, Cost Runtime: 3688 ms, Cost Memory: 16.2 MB) :
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        # search palindrome in the substrings from the longest to the shortest
        for offset in reversed(range(n)):
            for index_start in range(n-offset):
                index_end = index_start + offset
                if self.isPalindrome(index_start, index_end, s):
                    return s[index_start:index_end+1]

        return ''

    def isPalindrome(self, start: int, end: int, s: str) -> bool:
        while start < end:
            if s[start] != s[end]:
                return False

            start += 1
            end -= 1

        return True
```

Method 4 (DFS + Memoization (by Dictionary), Time Complexity: $O(N^3)$, Cost Runtime: 6851 ms, Cost Memory: 80.9 MB) :
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

Method 5 (DFS + Memoization (by List), Time Complexity: $O(N^3)$, Cost Runtime: 3838 ms, Cost Memory: 24.7 MB) :
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

Method 6 (From Center + Two Pointers, Time Complexity: $O(N^2)$) :
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

Method 7 (From Center + Two Pointers, Time Complexity: $O(N^3)$) :
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        result = ''
        for index_center in range(n):
            temp = self.maximumPalindrome(index_center, index_center, s)
            if index_center < n-1:
                temp_even = self.maximumPalindrome(index_center, index_center+1, s)
                if len(temp_even) > len(temp):
                    temp = temp_even

            if len(result) < len(temp):
                result = temp

        return result

    def maximumPalindrome(self, index_center_left: int, index_center_right: int, s: str) -> str:
        n = len(s)
        while index_center_left >= 0 and index_center_right < n and s[index_center_left] == s[index_center_right]:
            index_center_left -= 1
            index_center_right += 1

        return s[index_center_left+1:index_center_right]
```

Method 8 (Dynamic Programming, Time Complexity: $O(N^2)$) :
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        result = [0, 0]
        dp = [[False]*n for _ in range(n)]
        dp[-1][-1] = True
        for index in range(n-1):
            dp[index][index] = True
            if s[index] == s[index+1]:
                dp[index][index+1] = True
                result = [index, index+1]

        # iteratively search the substrings in the range of [index_start, index_end] are palindromes or not
        for offset in range(2, n):
            for index_start in range(n-offset):
                index_end = index_start + offset
                if s[index_start] == s[index_end] and dp[index_start+1][index_end-1]:
                    dp[index_start][index_end] = True
                    result = [index_start, index_end]

        return s[result[0]:result[1]+1]
```
