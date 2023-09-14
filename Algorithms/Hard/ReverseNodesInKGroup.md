![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 25. [Reverse Nodes In K Group](https://leetcode.com/problems/reverse-nodes-in-k-group)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Brute Force + Record Each Nodes In The Groups) :
```python
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        if head is None:
            return head

        groups = []
        group = []
        node = head
        while node:
            group.append(node)
            if len(group) == k:
                groups.append(group)
                group = []
            node = node.next
        if len(group):
            groups.append(group)

        head_new = None
        previous_tail = None
        for index_group in range(len(groups)):
            if len(groups[index_group]) == k:
                head_group, tail_group = self.reverseNodesInGroup(groups[index_group])
            else:
                head_group, tail_group = groups[index_group][0], groups[index_group][-1]

            if head_new is None:
                head_new = head_group
            if previous_tail:
                previous_tail.next = head_group

            previous_tail = tail_group

        return head_new

    def reverseNodesInGroup(self, nodes: List[ListNode]) -> Tuple[ListNode]:
        dummyHead = node = ListNode()
        for node_group in reversed(nodes):
            node.next = node_group
            node = node.next
        node.next = None

        return (dummyHead.next, node)
```

Method 2 (Reverse In The Loop) :
```python
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        if head is None:
            return head

        group = []
        node = head
        head_new = None
        previous_tail = None
        while node:
            group.append(node)
            node = node.next
            if len(group) == k:
                head_group, tail_group = self.reverseNodesInGroup(group)
                group = []

                if head_new is None:
                    head_new = head_group
                if previous_tail:
                    previous_tail.next = head_group

                previous_tail = tail_group

        if len(group):
            head_group, tail_group = group[0], group[-1]
            if head_new is None:
                return head_group

            if previous_tail:
                previous_tail.next = head_group

        return head_new

    def reverseNodesInGroup(self, nodes: List[ListNode]) -> Tuple[ListNode]:
        dummyHead = node = ListNode()
        for node_group in reversed(nodes):
            node.next = node_group
            node = node.next
        node.next = None

        return (dummyHead.next, node)
```

Method 3 (Reverse) :
```python
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        nodeDummy = ListNode(next=head)
        amount = 0

        node = nodePreviousTail = nodeDummy
        while node.next:
            node = node.next
            amount += 1
            if amount != k:
                continue

            node = self.reverseNodes(nodePreviousTail, node)
            nodePreviousTail = node
            amount = 0

        return nodeDummy.next

    def reverseNodes(self, nodePrevious, nodeHeadNew):
        nodeStart = nodePrevious.next
        while nodePrevious.next is not nodeHeadNew:
            nodeNext = nodeStart.next
            nodeStart.next = nodeNext.next
            nodeNext.next = nodePrevious.next
            nodePrevious.next = nodeNext

        # this node is the reversed tail
        return nodeStart
```

### Solution :

```php
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val = 0, $next = null) {
 *         $this->val = $val;
 *         $this->next = $next;
 *     }
 * }
 */
```

Method 1 (Reverse) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $k
     * @return ListNode
     */
    function reverseKGroup($head, $k) {
        $dummyHead = $node = $nodePreviousTail = new ListNode(0, $head);

        $counter = 0;
        while($node->next) {
            $node = $node->next;
            $counter++;

            if ($counter < $k) {
                continue;
            }

            $node = $nodePreviousTail = $this->reverseNodes($nodePreviousTail, $node);
            $counter = 0;
        }

        return $dummyHead->next;
    }

    function reverseNodes($nodePreviousTail, $nodeCurrentTail) {
        $nodeCurrent = $nodePreviousTail->next;
        while ($nodePreviousTail->next !== $nodeCurrentTail) {
            $nodeNext = $nodeCurrent->next;
            $nodeCurrent->next = $nodeNext->next;
            $nodeNext->next = $nodePreviousTail->next;
            $nodePreviousTail->next = $nodeNext;
        }

        return $nodeCurrent;
    }
}
```
