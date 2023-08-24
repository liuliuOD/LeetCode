![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 92. [Reverse Linked List II](https://leetcode.com/problems/swapping-nodes-in-a-linked-list)

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

Method 1 (Replace Values) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $left
     * @param Integer $right
     * @return ListNode
     */
    function reverseBetween($head, $left, $right) {
        $temp = new ListNode(0, $head);
        for ($index=0; $index < $left; $index++) {
            $temp = $temp->next;
        }

        $values = $this->getValuesInRange($temp, $right-$left+1);

        foreach ($values as $value) {
            $temp->val = $value;
            $temp = $temp->next;
        }

        return $head;
    }

    function getValuesInRange($node, $offset) {
        $values = [];
        while ($offset) {
            $offset--;
            $values[] = $node->val;
            $node = $node->next;
        }

        return array_reverse($values);
    }
}
```
