![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 160. [Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
```

Method 1 (Merge 2 Linked Lists) :
```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        pointerA, pointerB = headA, headB
        while pointerA != pointerB:
            pointerA = pointerA.next if pointerA else headB
            pointerB = pointerB.next if pointerB else headA
        return pointerA
```

Method 2 (Transfer Linked List A to cycle) :
```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        pointerSlow = pointerFast = headB
        pointerCycle = headA
        while True:
            if pointerCycle.next is None:
                pointerCycle.next = headA
                break
            pointerCycle = pointerCycle.next

        while True:
            if pointerSlow is None or pointerFast is None:
                pointerCycle.next = None
                return None

            pointerSlow = pointerSlow.next
            pointerFast = pointerFast.next
            if pointerFast is None:
                pointerCycle.next = None
                return None

            pointerFast = pointerFast.next
            if pointerSlow == pointerFast:
                break

        pointerSlow = headB
        while pointerSlow != pointerFast:
            pointerSlow = pointerSlow.next
            pointerFast = pointerFast.next
        
        pointerCycle.next = None

        return pointerSlow
```
