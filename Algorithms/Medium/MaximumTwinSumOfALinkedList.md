![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2130. [Maximum Twin Sum Of A Linked List](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Fast-slow Pointers + Stack) :
```python
class Solution:
    def pairSum(self, head: Optional[ListNode]) -> int:
        twins = [head.val]
        pointer_slow = head
        pointer_fast = head.next
        while pointer_fast and pointer_fast.next:
            pointer_slow = pointer_slow.next
            pointer_fast = pointer_fast.next.next

            twins.append(pointer_slow.val)

        result = 0
        pointer_slow = pointer_slow.next
        while pointer_slow:
            result = max(result, twins.pop() + pointer_slow.val)
            pointer_slow = pointer_slow.next
        return result
```

Method 2 (Fast-slow Pointers + Reverse LinkedList) :
```python
class Solution:
    def pairSum(self, head: Optional[ListNode]) -> int:
        pointer_slow = head
        pointer_fast = head
        while pointer_fast and pointer_fast.next:
            pointer_slow = pointer_slow.next
            pointer_fast = pointer_fast.next.next
        
        pointer_next = prev = None
        while pointer_slow:
            pointer_next = pointer_slow.next
            pointer_slow.next = prev
            prev = pointer_slow
            pointer_slow = pointer_next
        
        result = 0
        while prev and head:
            result = max(result, prev.val + head.val)
            prev = prev.next
            head = head.next
        return result
```
