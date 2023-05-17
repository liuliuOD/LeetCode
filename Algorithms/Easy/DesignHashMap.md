![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 706. [Design Hash Map](https://leetcode.com/problems/design-hashmap)

### Solution :

```python
# Your MyHashMap object will be instantiated and called as such:
# obj = MyHashMap()
# obj.put(key,value)
# param_2 = obj.get(key)
# obj.remove(key)
```

Method 1 (Linked List) :
```python
class MyHashMap:

    def __init__(self):
        self.head = ListNode(val=None)

    def put(self, key: int, value: int) -> None:
        node = self.head
        while node and node.next:
            if node.next.key == key:
                node.next.val = value
                return
            node = node.next
        node.next = ListNode(key=key, val=value)

    def get(self, key: int) -> int:
        node = self.head
        while node and node.next:
            if node.next.key == key:
                return node.next.val
            node = node.next
        return -1

    def remove(self, key: int) -> None:
        node = self.head
        while node and node.next:
            if node.next.key == key:
                node.next = node.next.next
                return
            node = node.next
        
class ListNode:
    def __init__(self, key=None, val=0, next=None):
        self.key = key
        self.val = val
        self.next = next
```
