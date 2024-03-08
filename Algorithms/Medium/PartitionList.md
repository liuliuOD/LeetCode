![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 86. [Partition List](https://leetcode.com/problems/partition-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (2 List, create new nodes) :
```python
BASELINE = -101
class Solution:
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        head_smaller = ListNode(val=BASELINE)
        head_same_or_greater = ListNode(val=BASELINE)
        pointer_smaller = head_smaller
        pointer_same_or_greater = head_same_or_greater
        while head:
            if head.val < x:
                pointer_smaller.next = ListNode(val=head.val)
                pointer_smaller = pointer_smaller.next
            elif head.val >= x:
                pointer_same_or_greater.next = ListNode(val=head.val)
                pointer_same_or_greater = pointer_same_or_greater.next
            head = head.next

        # if there are nodes >= x then merge 2 List
        if head_same_or_greater.next:
            pointer_smaller.next = head_same_or_greater.next

        return head_smaller.next
```

Method 2 (2 List, use original nodes) :
```python
BASELINE = -101
class Solution:
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        head_smaller = ListNode(val=BASELINE)
        head_same_or_greater = ListNode(val=BASELINE)
        pointer_smaller = head_smaller
        pointer_same_or_greater = head_same_or_greater
        while head:
            if head.val < x:
                pointer_smaller.next = head
                pointer_smaller = pointer_smaller.next
            elif head.val >= x:
                pointer_same_or_greater.next = head
                pointer_same_or_greater = pointer_same_or_greater.next

            head = head.next

        # remove head.next
        pointer_same_or_greater.next = None
        pointer_smaller.next = head_same_or_greater.next

        return head_smaller.next
```
