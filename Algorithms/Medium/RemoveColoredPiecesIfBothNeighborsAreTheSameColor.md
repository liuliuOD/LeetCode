![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2038. [Remove Colored Pieces If Both Neighbors Are The Same Color](https://leetcode.com/problems/remove-colored-pieces-if-both-neighbors-are-the-same-color)

### Solution :

Method 1 :
```python
class Solution:
    def winnerOfGame(self, colors: str) -> bool:
        amount_AAA = amount_BBB = 0
        for index in range(len(colors)-2):
            if colors[index:index+3] == 'AAA':
                amount_AAA += 1
            elif colors[index:index+3] == 'BBB':
                amount_BBB += 1

        return amount_AAA > amount_BBB
```

Method 2 (Switch Case) :
```python
class Solution:
    def winnerOfGame(self, colors: str) -> bool:
        amount_AAA = amount_BBB = 0
        for index in range(len(colors)-2):
            match colors[index:index+3]:
                case 'AAA':
                    amount_AAA += 1
                    continue
                case 'BBB':
                    amount_BBB += 1

        return amount_AAA > amount_BBB
```

Method 3 :
```python
class Solution:
    def winnerOfGame(self, colors: str) -> bool:
        amount = 0
        for index in range(len(colors)-2):
            match colors[index:index+3]:
                case 'AAA':
                    amount += 1
                    continue
                case 'BBB':
                    amount -= 1

        return amount > 0
```

Method 4 (use Built-In method) :
```python
class Solution:
    def winnerOfGame(self, colors: str) -> bool:
        result = 0
        for char, group in groupby(colors):
            amount = max(0, len(list(group)) - 2)
            if char == 'A':
                result += amount
            elif char == 'B':
                result -= amount

        return result > 0
```
