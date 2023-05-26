![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 19. [Remove Nth Node From End Of List](https://leetcode.com/problems/add-two-numbers)

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
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(next=head)
        pointer_slow = dummy
        pointer_fast = dummy
        for i in range(n):
            pointer_fast = pointer_fast.next
        while pointer_fast.next:
            pointer_fast = pointer_fast.next
            pointer_slow = pointer_slow.next
        pointer_slow.next = pointer_slow.next.next
        return dummy.next
```
