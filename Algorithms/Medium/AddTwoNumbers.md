![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2. [Add Two Numbers](https://leetcode.com/problems/add-two-numbers)

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
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        head = ListNode()
        current = head
        carry = 0
        while l1 or l2 or carry:
            if not l1:
                l1 = ListNode()
            if not l2:
                l2 = ListNode()
            val = carry + l1.val + l2.val
            carry = val // 10
            current.next = ListNode(val=val%10)
            current = current.next
            l1 = l1.next
            l2 = l2.next
        return head.next
```
