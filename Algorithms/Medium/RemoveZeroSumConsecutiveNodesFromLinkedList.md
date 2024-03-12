![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 1171. [Remove Zero Sum Consecutive Nodes From Linked List](https://leetcode.com/problems/remove-zero-sum-consecutive-nodes-from-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def removeZeroSumSublists(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(next=head)
        start = dummy
        while start:
            summarize = 0
            next_node = start.next
            while next_node:
                summarize += next_node.val
                if summarize == 0:
                    start.next = next_node.next

                next_node = next_node.next

            start = start.next

        return dummy.next
```

Method 2 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def removeZeroSumSublists(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(val=0,next=head)

        prefix_sum = {}
        summarize = 0
        current = dummy
        while current:
            summarize += current.val
            if summarize in prefix_sum:
                target = current
                current = prefix_sum[summarize].next
                summarize_temp = summarize
                while current is not target:
                    summarize_temp += current.val
                    if summarize_temp in prefix_sum:
                        del prefix_sum[summarize_temp]

                    current = current.next

                prefix_sum[summarize].next = current.next
            else:
                prefix_sum[summarize] = current

            current = current.next

        return dummy.next
```

### Solution :

```go
/*
// Definition for singly-linked list.
type ListNode struct {
    Val int
    Next *ListNode
}
*/
```

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```go
func removeZeroSumSublists(head *ListNode) *ListNode {
    dummy := &ListNode{Val: 0, Next: head}
    for start := dummy; start != nil; start = start.Next {
        sum := 0
        for next := start.Next; next != nil; next = next.Next {
            sum += next.Val
            if sum == 0 {
                start.Next = next.Next
            }
        }
    }

    return dummy.Next
}
```
