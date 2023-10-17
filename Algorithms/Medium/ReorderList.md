![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 143. [Reorder List](https://leetcode.com/problems/reorder-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Hash Map) :
```python
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        mapping = []
        dummy_head = ListNode(next=head)
        while dummy_head.next:
            dummy_head = dummy_head.next
            mapping.append(dummy_head)

        mapping.reverse()
        n = len(mapping)
        index = 0
        dummy_head = head
        while dummy_head.next:
            node_temp = dummy_head.next
            if dummy_head == mapping[index]:
                dummy_head.next = None
                break

            dummy_head.next = mapping[index]
            if mapping[index] == node_temp:
                node_temp.next = None
                break
            mapping[index].next = node_temp
            dummy_head = node_temp
            index += 1
```

Method 2 (Slow & Fast Pointers + Reverse Nodes) :
```python
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        amount = 1
        slow, fast = head, head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
            amount += 2 if fast else 1

        reversed_middle = self.reverseList(slow)
        while reversed_middle:
            temp_head = head.next
            temp_reversed_middle = reversed_middle.next

            head.next = reversed_middle
            reversed_middle.next = temp_head

            head = temp_head
            reversed_middle = temp_reversed_middle

        if amount % 2 == 0:
            head.next = None

    def reverseList(self, head):
        dummy = ListNode(next=head)
        node_current = head
        while node_current.next:
            node_next = node_current.next
            node_current.next = node_next.next
            node_next.next = dummy.next
            dummy.next = node_next

        return dummy.next
```
