![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1290. [Convert Binary Number In A Linked List To Integer](https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (list + join) :
```python
class Solution:
    def getDecimalValue(self, head: ListNode) -> int:
        binary_list = []
        while head:
            binary_list.append(head.val)
            head = head.next
        return int(''.join(map(str, binary_list)), 2)
```

Method 2 (string) :
```python
class Solution:
    def getDecimalValue(self, head: ListNode) -> int:
        binary_string = ''
        while head:
            binary_string += str(head.val)
            head = head.next
        return int(binary_string, 2)
```
