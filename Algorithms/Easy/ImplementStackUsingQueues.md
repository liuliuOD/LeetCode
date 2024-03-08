![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 225. [Implement Stack Using Queues](https://leetcode.com/problems/implement-stack-using-queues)

### Solution :

```python
# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```

Method 1 (Queue, with method pop) :
```python
class MyStack:

    def __init__(self):
        self.queue = deque()

    def push(self, x: int) -> None:
        self.queue.append(x)

    def pop(self) -> int:
        result = self.queue.pop()
        return result

    def top(self) -> int:
        return self.queue[-1]

    def empty(self) -> bool:
        return len(self.queue) == 0
```

Method 2 (Queue, without any methods not include in queue) :
```python
class MyStack:

    def __init__(self):
        self.queue = deque()

    def push(self, x: int) -> None:
        self.queue.append(x)
        for _ in range(len(self.queue)-1):
            self.queue.append(self.queue.popleft())

    def pop(self) -> int:
        return self.queue.popleft()

    def top(self) -> int:
        return self.queue[0]

    def empty(self) -> bool:
        return len(self.queue) == 0
```

### Solution :

```php
/**
 * Your MyStack object will be instantiated and called as such:
 * $obj = MyStack();
 * $obj->push($x);
 * $ret_2 = $obj->pop();
 * $ret_3 = $obj->top();
 * $ret_4 = $obj->empty();
 */
```

Method 1 (Queue) :
```php
class MyStack {
    /**
     */
    function __construct() {
        $this->queue = new SplQueue();
    }
  
    /**
     * @param Integer $x
     * @return NULL
     */
    function push($x) {
        $this->queue->push($x);
    }
  
    /**
     * @return Integer
     */
    function pop() {
        return $this->queue->pop();
    }
  
    /**
     * @return Integer
     */
    function top() {
        return $this->queue->top();
    }
  
    /**
     * @return Boolean
     */
    function empty() {
        return $this->queue->isEmpty();
    }
}
```
