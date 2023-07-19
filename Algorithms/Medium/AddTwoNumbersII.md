![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 445. [Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Reverse Linked List) :
```python
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        l1 = self.reverseLinkedList(l1)
        l2 = self.reverseLinkedList(l2)

        result = self.addNodes(l1, l2)

        return self.reverseLinkedList(result)

    def reverseLinkedList(self, l: ListNode) -> ListNode:
        root = None
        while l and l.val is not None:
            temp = root
            root = l
            node_next = l.next
            l.next = temp
            l = node_next
        return root

    def addNodes(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> int:
        carry = 0
        root = result_node = ListNode()
        while l1 or l2:
            is_none_l1 = l1 is None
            is_none_l2 = l2 is None
            if is_none_l1:
                l1 = ListNode(val=0)
            if is_none_l2:
                l2 = ListNode(val=0)

            sum_nodes = carry + l1.val + l2.val
            carry = sum_nodes // 10

            l1 = l1.next
            l2 = l2.next

            result_node.val = sum_nodes % 10
            temp = ListNode(val=None)
            result_node.next = temp
            result_node = result_node.next

        if carry:
            result_node.val = carry

        return root
```

Method 2 (Reverse Linked List) :
```python
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        l1 = self.reverseLinkedList(l1)
        l2 = self.reverseLinkedList(l2)

        return self.addNodes(l1, l2)

    def reverseLinkedList(self, l: ListNode) -> ListNode:
        root = None
        while l:
            temp = root
            root = l
            node_next = l.next
            l.next = temp
            l = node_next
        return root

    def addNodes(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> int:
        carry = 0
        result_node = None
        while l1 or l2:
            is_none_l1 = l1 is None
            is_none_l2 = l2 is None
            if is_none_l1:
                l1 = ListNode(val=0)
            if is_none_l2:
                l2 = ListNode(val=0)

            sum_nodes = carry + l1.val + l2.val
            carry = sum_nodes // 10

            l1 = l1.next
            l2 = l2.next

            node = ListNode(val=sum_nodes%10, next=result_node)
            result_node = node

        if carry:
            node = ListNode(val=carry, next=result_node)
            result_node = node

        return result_node
```

Method 3 (Stack) :
```python
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        stack_l1 = self.setStack(l1)
        stack_l2 = self.setStack(l2)

        return self.addTwoStack(stack_l1, stack_l2)

    def setStack(self, l: Optional[ListNode]) -> List[int]:
        stack = list()
        while l:
            stack.append(l.val)
            l = l.next
        return stack

    def addTwoStack(self, stack_1: List[int], stack_2: List[int]) -> ListNode:
        carry = 0
        root = None
        while stack_1 or stack_2:
            value_1 = stack_1.pop() if stack_1 else 0
            value_2 = stack_2.pop() if stack_2 else 0

            sum_value = carry + value_1 + value_2
            node = ListNode(val=sum_value%10, next=root)
            root = node

            carry = sum_value // 10

        if carry:
            node = ListNode(val=carry, next=root)
            root = node

        return root
```
