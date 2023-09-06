![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 725. [Split Linked List In Parts](https://leetcode.com/problems/split-linked-list-in-parts)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Traverse) :
```python
class Solution:
    def splitListToParts(self, head: Optional[ListNode], k: int) -> List[Optional[ListNode]]:
        amount_nodes = 0
        node = head
        while node:
            amount_nodes += 1
            node = node.next

        result = [ListNode() for _ in range(k)]
        head_result = result[0]
        index_divide = 0
        divides = [amount_nodes // k + (1 if index < amount_nodes % k else 0) for index in range(k)]
        node = head
        while node:
            head_result.next = node
            head_result = head_result.next

            node = node.next

            divides[index_divide] -= 1
            if divides[index_divide] == 0 and index_divide+1 < len(divides):
                head_result.next = None
                index_divide += 1
                head_result = result[index_divide]

        return [node.next for node in result]
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

Method 1 (Traverse) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $k
     * @return ListNode[]
     */
    function splitListToParts($head, $k) {
        $nodeAmount = 0;
        $node = $head;
        while ($node) {
            $node = $node->next;
            $nodeAmount++;
        }

        $resultAmount = [];
        for ($i = 0; $i < $k; $i++) {
            $amount = intval($nodeAmount / $k);
            if ($nodeAmount % $k > $i) {
                $amount++;
            }

            $resultAmount[] = $amount;
        }

        $result = array_fill(0, $k, null);
        $node = $head;
        $tempHead = null;
        $indexAmount = 0;
        while ($node) {
            if (is_null($tempHead)) {
                $tempHead = $node;
                $result[$indexAmount] = $tempHead;
            }

            if (--$resultAmount[$indexAmount] == 0) {
                $indexAmount++;
                $tempHead = null;
                $nodeTemp = $node->next;
                $node->next = null;
                $node = $nodeTemp;
                continue;
            }

            $node = $node->next;
        }

        return $result;
    }
}
```
