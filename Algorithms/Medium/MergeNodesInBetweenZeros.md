![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2181. [Merge Nodes In Between Zeros](https://leetcode.com/problems/merge-nodes-in-between-zeros)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def mergeNodes(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None:
            return head

        node_remaining = head
        node = head.next
        summarize = 0
        while node:
            summarize += node.val
            if node.val == 0 and summarize > 0:
                node_remaining.val = summarize
                summarize = 0
                if node.next:
                    node_remaining.next = node
                else:
                    node_remaining.next = None

                node_remaining = node

            node = node.next

        return head
```
