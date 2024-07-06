![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2058. [Find The Minimum And Maximum Number Of Nodes Between Critical Points](https://leetcode.com/problems/find-the-minimum-and-maximum-number-of-nodes-between-critical-points)

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

Method 1 (Time Complexity: $O(N)$ (N: number of the nodes in the linked list), Space Complexity: $O(1)$) :
```rust
type Custom = Option<Box<ListNode>>;
impl Solution {
    pub fn nodes_between_critical_points(head: Custom) -> Vec<i32> {
        return match head {
            None => vec![-1, -1],
            Some(inner_head) => {
                let mut previous: i32 = inner_head.val;
                let mut node: Custom = inner_head.next;
                let mut index_previous: usize = 0;
                let mut index_first: usize = 0;
                let mut index: usize = 1;
                let mut result_minimum: i32 = i32::MAX;

                while let Some(inner_current) = node {
                    match inner_current.next.as_ref() {
                        None => break,
                        Some(&ref inner_next) => {
                            if (previous < inner_current.val && inner_current.val > inner_next.val) || (previous > inner_current.val && inner_current.val < inner_next.val) {
                                if index_previous > 0 {
                                    result_minimum = i32::min(result_minimum, (index - index_previous) as i32);
                                }

                                if index_first == 0 {
                                    index_first = index;
                                }
                                index_previous = index;
                            }

                            previous = inner_current.val;
                            node = inner_current.next;
                        },
                    };

                    index += 1;
                }
                if index_previous > 0 && index_previous-index_first > 0 {
                    return vec![result_minimum, (index_previous-index_first) as i32]
                }
                return vec![-1, -1]
            },
        }
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

Method 1 (Brute Force, Time Complexity: $O(N)$ (N: amount of nodes in the linked list), Space Complexity: $O(N)$) :
```python
class Solution:
    def nodesBetweenCriticalPoints(self, head: Optional[ListNode]) -> List[int]:
        index_list: list[int] = []
        number = 1
        previous = None
        while head and head.next:
            if previous and ((previous < head.val and head.val > head.next.val) or (previous > head.val and head.val < head.next.val)):
                index_list.append(number)

            previous = head.val
            head = head.next
            number += 1

        return [min(b-a for a, b in pairwise(index_list)), index_list[-1]-index_list[0]] if len(index_list) >= 2 else [-1, -1]
```

Method 2 (Time Complexity: $O(N)$ (N: amount of nodes in the linked list), Space Complexity: $O(1)$) :
```python
class Solution:
    def nodesBetweenCriticalPoints(self, head: Optional[ListNode]) -> List[int]:
        index_first: int = None
        index_previous: int = None
        number = 1
        previous = head.val
        node = head.next
        minimum = inf
        while node.next:
            if (previous < node.val and node.val > node.next.val) or (previous > node.val and node.val < node.next.val):
                if index_previous is not None:
                    minimum = min(minimum, number-index_previous)

                if index_first is None:
                    index_first = number

                index_previous = number

            previous = node.val
            node = node.next
            number += 1

        return [-1, -1] if index_previous is None or minimum is inf else [minimum, index_previous-index_first]
```
