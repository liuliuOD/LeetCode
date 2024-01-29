![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 232. [Implement Queue Using Stacks](https://leetcode.com/problems/implement-queue-using-stacks)

### Solution :

```python
# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```

Method 1 (Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class MyQueue:

    def __init__(self):
        self.stack = []

    def push(self, x: int) -> None:
        self.stack.append(x)

    def pop(self) -> int:
        temp = []
        for index in reversed(range(len(self.stack))):
            temp.append(self.stack[index])

        front = temp.pop()

        current = []
        for index in reversed(range(len(temp))):
            current.append(temp[index])
        self.stack = current
        return front

    def peek(self) -> int:
        temp = []
        for index in reversed(range(len(self.stack))):
            temp.append(self.stack[index])

        front = temp.pop()
        temp.append(front)
        return front

    def empty(self) -> bool:
        return len(self.stack) == 0
```
