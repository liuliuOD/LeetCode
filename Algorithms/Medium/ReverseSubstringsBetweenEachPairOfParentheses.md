![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1190. [Reverse Substrings Between Each Pair Of Parentheses](https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: length of `s`)) :
```python
class Solution:
    def reverseParentheses(self, s: str) -> str:
        left = []
        pairs = []
        for index, char in enumerate(s):
            if char == '(':
                left.append(index)
            elif char == ')':
                pairs.append((left.pop(), index))

        result = s
        n = len(s)
        for left, right in pairs:
            substring = result[left:right]
            result = result[:left] + substring[::-1] + result[right:]

        return ''.join(filter(lambda char: char not in ['(', ')'], result))
```

Method 2 (Stack, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: length of `s`)) :
```python
class Solution:
    def reverseParentheses(self, s: str) -> str:
        stack = []
        result = []
        for index, char in enumerate(s):
            if char == "(":
                stack.append(len(result))
            elif char == ")":
                index_start = stack.pop()
                result[index_start:] = reversed(result[index_start:])
            else:
                result.append(char)

        return ''.join(result)
```
