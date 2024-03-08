![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 557. [Reverse Words In A String III](https://leetcode.com/problems/reverse-words-in-a-string-iii)

### Solution :

Method 1 (The Slowest) :
```python
class Solution:
    def reverseWords(self, s: str) -> str:
        result = ''
        index_previous = 0
        n = len(s)
        for index in range(n):
            if s[index] != ' ':
                continue

            result += s[::-1][n-index:n-index_previous] + ' '
            index_previous = index + 1

        if s[-1] != ' ':
            result += s[::-1][:n-index_previous]

        return result
```

Method 2 :
```python
class Solution:
    def reverseWords(self, s: str) -> str:
        result = []
        n = len(s)
        for word in s.split(' '):
            result.append(word[::-1])

        return ' '.join(result)
```

Method 3 :
```python
class Solution:
    def reverseWords(self, s: str) -> str:
        words = s.split(' ')
        for index in range(len(words)):
            words[index] = words[index][::-1]

        return ' '.join(words)
```
