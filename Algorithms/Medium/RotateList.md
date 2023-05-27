![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 61. [Rotate List](https://leetcode.com/problems/rotate-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Cycle then remove) :
```python
class Solution:
    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        if k == 0 or head is None:
            return head

        node_amount = 1
        node = head
        while node.next:
            node = node.next
            node_amount += 1
        # set list to cycle
        node.next = head

        k = k % node_amount
        node = head
        for _ in range(node_amount - k):
            tail = node
            node = node.next
        tail.next = None

        return node
```

Method 2 :
```python
class Solution:
    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        if k == 0 or head is None:
            return head

        node_amount = 1
        node = head
        while node.next:
            node = node.next
            node_amount += 1
        # set list to cycle
        node.next = head

        k = k % node_amount
        node = head
        for _ in range(node_amount - k - 1):
            node = node.next
        result, node.next = node.next, None

        return result
```
