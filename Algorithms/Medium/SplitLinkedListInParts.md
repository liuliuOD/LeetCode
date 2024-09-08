![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 725. [Split Linked List In Parts](https://leetcode.com/problems/split-linked-list-in-parts)

### Solution :

```rust
// Definition for singly-linked list.
// #[derive(PartialEq, Eq, Clone, Debug)]
// pub struct ListNode {
//   pub val: i32,
//   pub next: Option<Box<ListNode>>
// }
//
// impl ListNode {
//   #[inline]
//   fn new(val: i32) -> Self {
//     ListNode {
//       next: None,
//       val
//     }
//   }
// }
```

Method 1 (Traverse, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in the linked list)) :
```rust
type Custom = Box<ListNode>;
impl Solution {
    pub fn split_list_to_parts(mut head: Option<Custom>, k: i32) -> Vec<Option<Custom>> {
        let mut n: usize = 0;
        Self::traverse(&head, &mut n);

        let k: usize = k as usize;
        let mut n_each: usize = n / k;
        let mut n_remaining: usize = n % k;
        let mut result: Vec<Option<Custom>> = Vec::new();
        for index in 0..k {
            if head.is_none() {
                result.push(None);
            } else {
                result.push(head.take());
                let mut amount: usize = 1;
                if index < n_remaining {
                    amount -= 1;
                }
                let mut current: &mut Custom = result[index].as_mut().unwrap();
                while let Some(inner) = current.next.take() {
                    if amount == n_each {
                        head = Some(inner);
                    } else {
                        amount += 1;
                        current.next = Some(inner);
                        current = current.next.as_mut().unwrap();
                    }
                }
            }
        }

        return result
    }

    fn traverse(head: &Option<Custom>, n: &mut usize) {
        if head.is_none() {
            return
        }

        *n += 1;
        return Self::traverse(&head.as_ref().unwrap().next, n)
    }
}
```

Method 2 (Traverse, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in the linked list)) :
```rust
type Custom = Box<ListNode>;
impl Solution {
    pub fn split_list_to_parts(mut head: Option<Custom>, k: i32) -> Vec<Option<Custom>> {
        let mut n: usize = 0;
        Self::traverse(&head, &mut n);

        let k: usize = k as usize;
        let mut n_each: usize = n / k;
        let mut n_remaining: usize = n % k;
        let mut result: Vec<Option<Custom>> = Vec::new();
        for index in 0..k {
            match head {
                None => result.push(None),
                _ => {
                    result.push(head.take());
                    let mut amount: usize = (index >= n_remaining) as usize;
                    let mut current: &mut Custom = result[index].as_mut().unwrap();
                    while current.next.is_some() {
                        if amount == n_each {
                            head = current.next.take();
                        } else {
                            amount += 1;
                            current = current.next.as_mut().unwrap();
                        }
                    }
                },
            }
        }

        return result
    }

    fn traverse(head: &Option<Custom>, n: &mut usize) {
        if head.is_none() {
            return
        }

        *n += 1;
        return Self::traverse(&head.as_ref().unwrap().next, n)
    }
}
```

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
