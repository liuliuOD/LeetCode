![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
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

Method 2 (Array List + Linked List, (as the size decreases, the speed also decreases)) :
```python
class ListNode:

    def __init__(self, key=None, val=None, next=None):
        self.key = key
        self.val = val
        self.next = next

class MyHashMap:

    def __init__(self, size=10000):
        """
        Data Structure in self.mapping
        [None, ListNode, None, ...]
         |   , |       , |   , ...
         ˇ     ˇ         ˇ
         x   , None    , x   , ...
        """
        self.mapping = [None] * size

    def __index(self, key: int) -> int:
        return key % len(self.mapping)

    def put(self, key: int, value: int) -> None:
        index = self.__index(key)
        if self.mapping[index] is None:
            self.mapping[index] = ListNode(key, value)
            return

        node = self.mapping[index]
        while node:
            if node.key == key:
                node.val = value
                return

            if node.next is None:
                break
            node = node.next

        node.next = ListNode(key, value)

    def get(self, key: int) -> int:
        index = self.__index(key)
        node = self.mapping[index]
        while node:
            if node.key == key:
                return node.val

            node = node.next

        return -1

    def remove(self, key: int) -> None:
        index = self.__index(key)
        if self.mapping[index] is None:
            return

        dummyHead = node = ListNode(next=self.mapping[index])
        while node.next:
            if node.next.key == key:
                node.next = node.next.next
                break

            node = node.next

        self.mapping[index] = dummyHead.next
```
