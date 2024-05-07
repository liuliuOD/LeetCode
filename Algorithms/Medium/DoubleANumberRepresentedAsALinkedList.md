![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2816. [Double A Number Represented As A Linked List](https://leetcode.com/problems/double-a-number-represented-as-a-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Traverse + Recreate, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def doubleIt(self, head: Optional[ListNode]) -> Optional[ListNode]:
        value = self.doubleValues(head).strip()

        if len(value) > 1:
            value = value.lstrip('0')
        if len(value) == 0:
            value = "0"

        return self.createList(value)

    def doubleValues(self, node: Optional[ListNode]) -> int:
        result = "0"
        while node:
            double = node.val * 2
            result = result[:-1] + str(int(result[-1])+double//10) + str(double%10)
            node = node.next
        return result

    def createList(self, value: str) -> Optional[ListNode]:
        root = ListNode()
        node = root
        for index in range(len(value)):
            temp = ListNode(val=int(value[index]))
            node.next = temp
            node = temp

        return root.next
```
