![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 138. [Copy List With Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer)

### Solution :

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""
```

Method 1 (Hash Table) :
```python
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        mapping = dict()
        head_copy = node_copy = Node(x=0)
        while head:
            node = Node(x=head.val, random=head.random)
            mapping[head] = node
            node_copy.next = node
            node_copy = node
            head = head.next

        node_copy = head_copy
        while node_copy and node_copy.next:
            node_copy = node_copy.next
            node_copy.random = mapping[node_copy.random] if node_copy.random in mapping else None

        return head_copy.next
```

Method 2 (Hash Table) :
```python
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        mapping = {None: None}
        node = head
        while node:
            mapping[node] = Node(x=node.val)
            node = node.next

        node = head
        while node:
            mapping[node].next = mapping[node.next]
            mapping[node].random = mapping[node.random]
            node = node.next

        return mapping[head]
```

Method 3 (Interweaving Node) :
```python
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        node = head
        while node:
            node.next = Node(x=node.val, next=node.next)
            node = node.next.next

        node = head
        while node and node.next:
            if node.random:
                node.next.random = node.random.next
            node = node.next.next

        node = head
        head_copy = node_copy = Node(x=0)
        while node and node.next:
            node_copy.next = node.next
            node_copy = node_copy.next
            node = node.next.next

        return head_copy.next
```

### Solution :

```php
/**
 * Definition for a Node.
 * class Node {
 *     public $val = null;
 *     public $next = null;
 *     public $random = null;
 *     function __construct($val = 0) {
 *         $this->val = $val;
 *         $this->next = null;
 *         $this->random = null;
 *     }
 * }
 */
```

Method 1 (Hash Table, ERROR: "PHP Fatal error:  Uncaught TypeError: spl_object_hash(): Argument #1 ($object) must be of type object, null given in solution.php") :
```php
class Solution {
    /**
     * @param Node $head
     * @return Node
     */
    function copyRandomList($head) {
        $mapping = [];
        $headDummy = $nodeCopy = new Node();
        while ($head) {
            $node = new Node($head->val);
            $mapping[$this->getHashByObject($head)] = $node;
            $nodeCopy->next = $node;
            $nodeCopy->random = $head->random;
            $nodeCopy = $node;
            $head = $head->next;
        }

        $nodeCopy = $headDummy;
        while ($nodeCopy && $nodeCopy->next) {
            $nodeCopy = $nodeCopy->next;

            if ($nodeCopy->random && isset($mapping[$this->getHashByObject($nodeCopy->random)])) {
                $nodeCopy->random = $mapping[$this->getHashByObject($nodeCopy->random)];
            }
        }

        return $headDummy->next;
    }

    function getHashByObject($obj) {
        return spl_object_hash($obj);
    }
}
```
