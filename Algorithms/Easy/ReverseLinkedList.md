![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 206. [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Dummy Pointer) :
```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None:
            return head

        dummy = ListNode()
        cur = head
        while cur:
            temp = cur.next
            cur.next = dummy
            cur, dummy = temp, cur

        head.next = None
        return dummy
```
