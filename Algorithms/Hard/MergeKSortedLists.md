![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 23. [Merge K Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Min Heap) :
```python
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        dummy_head = node = ListNode()
        min_heap = []
        counter = 0
        for head in lists:
            if not head:
                continue

            # heap in python compare from left to right if previous values are equivalent
            heapq.heappush(min_heap, (head.val, counter, head))
            counter += 1

        while min_heap:
            value, _, node_list = heapq.heappop(min_heap)
            node.next = ListNode(val=value)
            node = node.next

            node_next = node_list.next
            if node_next:
                heapq.heappush(min_heap, (node_next.val, counter, node_next))
                counter += 1

        return dummy_head.next
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

Method 1 (Brute Force) :
```php
class Solution {

    /**
     * @param ListNode[] $lists
     * @return ListNode
     */
    function mergeKLists($lists) {
        $nums = [];
        foreach ($lists as $node) {
            while ($node) {
                $nums[] = $node->val;
                $node = $node->next;
            }
        }

        sort($nums);
        $dummyHead = $node = new ListNode();
        foreach ($nums as $num) {
            $node->next = new ListNode($num);
            $node = $node->next;
        }

        return $dummyHead->next;
    }
}
```

Method 2 (Min Heap) :
```php
class Solution {

    /**
     * @param ListNode[] $lists
     * @return ListNode
     */
    function mergeKLists($lists) {
        $n = count($lists);
        $dummyHead = $node = new ListNode();
        $minHeap = new SplMinHeap();
        for ($index = 0; $index < $n; $index++) {
            if (is_null($lists[$index])) {
                continue;
            }

            $minHeap->insert([$lists[$index]->val, $lists[$index]]);
        }

        while ($minHeap->count()) {
            list($value, $nodeHeap) = $minHeap->extract();
            $node->next = new ListNode($value);
            $node = $node->next;

            if ($nodeHeap->next) {
                $minHeap->insert([$nodeHeap->next->val, $nodeHeap->next]);
            }
        }

        return $dummyHead->next;
    }
}
```
