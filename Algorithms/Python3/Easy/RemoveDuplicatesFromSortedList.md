## [Remove Duplicates From Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list)

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
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        node = head
        while node:
            if node.next and node.val == node.next.val:
                node.next = node.next.next
                continue
            node = node.next
        
        return head
```
