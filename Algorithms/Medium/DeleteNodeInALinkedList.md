![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 237. [Delete Node In A Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
```

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        while node and node.next:
            node.val = node.next.val

            if node.next.next is None:
                node.next = None
            node = node.next
```

Method 2 (Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        node.val = node.next.val
        node.next = node.next.next
```

### Solution :

```php
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val) { $this->val = $val; }
 * }
 */
```

Method 1 :
```php
class Solution {
    /**
     * @param ListNode $node
     * @return 
     */
    function deleteNode($node) {
        $node->val = $node->next->val;
        $node->next = $node->next->next;
    }
}
```

### Solution :

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
```

Method 1 (Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```go
func deleteNode(node *ListNode) {
    node.Val = node.Next.Val
    node.Next = node.Next.Next
}
```
