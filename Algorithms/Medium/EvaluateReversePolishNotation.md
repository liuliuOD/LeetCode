![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 150. [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation)

### Solution :

Method 1 (Loop)
```python
SYMBOLS = ('+', '-', '*', '/')
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        amount_number = 0
        stack = [int(token) if token not in SYMBOLS else token for token in tokens]
        while len(stack) > 1:
            temp = []
            for token in stack:
                if token not in SYMBOLS:
                    amount_number += 1
                    temp.append(int(token))
                elif amount_number >= 2:
                    amount_number = 0
                    second = temp.pop()
                    first = temp.pop()
                    value = 0
                    if token == '+':
                        value = first + second
                    elif token == '-':
                        value = first - second
                    elif token == '*':
                        value = first * second
                    elif token == '/':
                        # We cannot use `first // second` because it will yield the wrong answer when one of the values is negative
                        value = int(first / second)

                    temp.append(value)
                else:
                    amount_number = 0
                    temp.append(token)

            stack = temp

        return stack[0]
```
