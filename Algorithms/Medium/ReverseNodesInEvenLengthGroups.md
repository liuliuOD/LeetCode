![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 2074. [Reverse Nodes In Even Length Groups](https://leetcode.com/problems/reverse-nodes-in-even-length-groups)

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
     * @return ListNode
     */
    function reverseEvenLengthGroups($head) {
        $amountGroup = 1;
        $amountCurrent = 0;
        $dummyHead = $node = new ListNode(0, $head);
        $nodePreviousTail = $node;
        while($node->next) {
            $node = $node->next;
            $amount++;

            if ($amount == $amountGroup || is_null($node->next)) {
                if ($amount%2 == 0) {
                    $nodePreviousTail = $this->reverseNodes($nodePreviousTail, $node);
                } else {
                    $nodePreviousTail = $node;
                }
                $node = $nodePreviousTail;

                $amountGroup++;
                $amount = 0;
            }
        }

        return $dummyHead->next;
    }

    function reverseNodes($previousTail, $currentTail) {
        $current = $previousTail->next;
        while ($previousTail->next !== $currentTail) {
            $next = $current->next;
            $current->next = $next->next;
            $next->next = $previousTail->next;
            $previousTail->next = $next;
        }

        return $current;
    }
}
```
