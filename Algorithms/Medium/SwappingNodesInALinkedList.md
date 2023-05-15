![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1721. [Swapping Nodes In A Linked List](https://leetcode.com/problems/swapping-nodes-in-a-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 :
```python
class Solution:
    def swapNodes(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        pointer_dummy = ListNode(0, head)
        pointer_slow = pointer_dummy
        pointer_fast = pointer_dummy

        pointer_fast = self.traverse(pointer_fast, k)
        pointer_left = pointer_fast

        while pointer_fast:
            pointer_slow = self.traverse(pointer_slow, 1)
            pointer_fast = self.traverse(pointer_fast, 1)

        (pointer_left.val, pointer_slow.val) = (pointer_slow.val, pointer_left.val)

        return head

    def traverse(self, pointer, k) -> Optional[ListNode]:
        for _ in range(0, k):
            pointer = pointer.next
        return pointer
```
