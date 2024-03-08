![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 146. [LRU Cache](https://leetcode.com/problems/lru-cache)

### Solution :

```python
# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```

Method 1 (Dictionary + Double-end queue, Time Complexity: $O(N)$) :
```python
class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.cache = defaultdict(int)
        self.recent_usage = deque()

    def get(self, key: int) -> int:
        result = -1
        if key in self.cache:
            self.put(key, None)
            result = self.cache[key]

        return result

    def put(self, key: int, value: Optional[int]) -> None:
        if self.recent_usage.count(key) > 0:
            self.recent_usage.remove(key)
        
        if value is not None:
            self.cache[key] = value
        
        self.recent_usage.appendleft(key)
        while len(self.recent_usage) > self.capacity:
            last_key = self.recent_usage.pop()
            del self.cache[last_key]
```

Method 2-1 (Doubly Linked-List + Dictionary, Time Complexity: $O(1)$) :
```python
class ListNode:
    def __init__(self, key: int, value: int):
        self.key = key
        self.value = value
        self.next = None
        self.previous = None

class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.head = None
        self.tail = None
        self.mapping: Dict[int, ListNode] = defaultdict(ListNode)

    def get(self, key: int) -> int:
        if key not in self.mapping:
            return -1
        
        node_remove = self.mapping[key]
        node_previous = node_remove.previous
        node_next = node_remove.next
        del self.mapping[key]

        if node_remove == self.head:
            self.head = node_next
        if node_remove == self.tail:
            self.tail = node_previous
        
        if node_previous:
            node_previous.next = node_next
        if node_next:
            node_next.previous = node_previous

        node = ListNode(key, node_remove.value)
        
        node.next = self.head
        if self.head:
            self.head.previous = node
        self.head = node

        if self.tail is None:
            self.tail = node

        self.mapping[key] = node
        return node.value

    def put(self, key: int, value: int) -> None:
        if key in self.mapping:
            node_remove = self.mapping[key]
            node_previous = node_remove.previous
            node_next = node_remove.next
            del self.mapping[key]

            if node_remove == self.head:
                self.head = node_next
            if node_remove == self.tail:
                self.tail = node_previous
            
            if node_previous:
                node_previous.next = node_next
            if node_next:
                node_next.previous = node_previous
        node = ListNode(key, value)
        
        node.next = self.head
        if self.head:
            self.head.previous = node
        self.head = node

        if self.tail is None:
            self.tail = node

        self.mapping[key] = node
        while len(self.mapping) > self.capacity:
            node_tail = self.tail
            self.tail = node_tail.previous
            self.tail.next = None

            del self.mapping[node_tail.key]
```

Method 2-2 (Refactor) :
```python
class ListNode:
    def __init__(self, key: int, value: int):
        self.key = key
        self.value = value
        self.next = None
        self.previous = None

class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.head = None
        self.tail = None
        self.mapping: Dict[int, ListNode] = defaultdict(ListNode)

    def get(self, key: int) -> int:
        if key not in self.mapping:
            return -1
        
        node_remove = self.removeNode(key)

        node = ListNode(key, node_remove.value)
        
        self.appendRecentUsageNode(node)

        return node.value

    def put(self, key: int, value: int) -> None:
        if key in self.mapping:
            self.removeNode(key)
        node = ListNode(key, value)

        self.appendRecentUsageNode(node)
        while len(self.mapping) > self.capacity:
            node_tail = self.tail
            self.tail = node_tail.previous
            self.tail.next = None

            del self.mapping[node_tail.key]

    def removeNode(self, key: int) -> ListNode:
        node_remove = self.mapping[key]
        node_previous = node_remove.previous
        node_next = node_remove.next
        del self.mapping[key]

        if node_remove == self.head:
            self.head = node_next
        if node_remove == self.tail:
            self.tail = node_previous
        
        if node_previous:
            node_previous.next = node_next
        if node_next:
            node_next.previous = node_previous
        
        return node_remove

    def appendRecentUsageNode(self, node: ListNode) -> None:
        node.next = self.head
        if self.head:
            self.head.previous = node
        self.head = node

        if self.tail is None:
            self.tail = node

        self.mapping[node.key] = node
```
