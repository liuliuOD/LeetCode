![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 844. [Backspace String Compare](https://leetcode.com/problems/backspace-string-compare)

### Solution :

Method 1 (Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        stack_s = []
        for char in s:
            if char == '#':
                if len(stack_s):
                    stack_s.pop()
                continue

            stack_s.append(char)

        stack_t = []
        for char in t:
            if char == '#':
                if len(stack_t):
                    stack_t.pop()
                continue

            stack_t.append(char)

        return ''.join(stack_s) == ''.join(stack_t)
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        index_s, index_t = len(s) - 1, len(t) - 1
        backspacing_s = backspacing_t = 0
        while True:
            while index_s >= 0 and (backspacing_s > 0 or s[index_s] == '#'):
                # Option 1
                if s[index_s] == '#':
                    backspacing_s += 1
                else:
                    backspacing_s -= 1
                """
                # Option 2

                backspacing_s += 1 if s[index_s] == '#' else -1
                """

                index_s -= 1

            while index_t >= 0 and (backspacing_t > 0 or t[index_t] == '#'):
                if t[index_t] == '#':
                    backspacing_t += 1
                else:
                    backspacing_t -= 1
                """
                # Option 2

                backspacing_t += 1 if t[index_t] == '#' else -1
                """

                index_t -= 1

            if index_s == index_t == -1:
                return True

            if s[index_s] == t[index_t]:
                index_s -= 1
                index_t -= 1
            else:
                return False
```

Method 3 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        index_s, index_t = len(s) - 1, len(t) - 1
        backspacing_s = backspacing_t = 0
        while True:
            index_s, backspacing_s = self.loop(index_s, backspacing_s, s)
            index_t, backspacing_t = self.loop(index_t, backspacing_t, t)

            # Option 1
            if index_s == index_t == -1:
                return True

            if s[index_s] == t[index_t]:
                index_s -= 1
                index_t -= 1
            else:
                return False
            """
            # Option 2

            if index_s >= 0 and index_t >= 0 and s[index_s] == t[index_t]:
                index_s -= 1
                index_t -= 1
                continue

            return index_s == index_t == -1
            """

    def loop(self, index: int, backspacing: int, string: str):
        while index >= 0 and (backspacing > 0 or string[index] == '#'):
            backspacing += 1 if string[index] == '#' else -1

            index -= 1

        return (index, backspacing)
```
