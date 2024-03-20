![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1669. [Merge In Between Linked Lists](https://leetcode.com/problems/merge-in-between-linked-lists)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Brute Force, Time Complexity: $O(M+N)$ (M: amount of nodes in `list1`, N: amount of nodes in `list2`), Space Complexity: $O(1)$) :
```python
class Solution:
    def mergeInBetween(self, list1: ListNode, a: int, b: int, list2: ListNode) -> ListNode:
        left = list1
        offset = b - a + 2
        while a > 1:
            left = left.next
            a -= 1

        right = left
        while offset > 0:
            right = right.next
            offset -= 1

        left.next = list2
        while list2.next:
            list2 = list2.next
        list2.next = right

        return list1
```
