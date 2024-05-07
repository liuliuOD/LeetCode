![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2816. [Double A Number Represented As A Linked List](https://leetcode.com/problems/double-a-number-represented-as-a-linked-list)

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

Method 1 (Traverse, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
type Custom = Option<Box<ListNode>>;
impl Solution {
    pub fn double_it(head: Custom) -> Custom {
        let mut temp: ListNode = ListNode::new(0);
        temp.next = head;
        let mut dummy: Custom = Some(Box::new(temp));
        let mut node: &mut Custom = &mut dummy;
        while let Some(inner) = node.as_mut() {
            inner.val = (2 * inner.val) % 10;
            if inner.next.is_some() && inner.next.as_ref().unwrap().val * 2 >= 10 {
                inner.val += 1;
            }

            node = &mut inner.next;
        }

        let inner: &Box<ListNode> = dummy.as_ref().unwrap();
        return match inner.val {
            1 => dummy,
            _ => dummy.unwrap().next,
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

Method 1 (Traverse + Recreate, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def doubleIt(self, head: Optional[ListNode]) -> Optional[ListNode]:
        value = self.doubleValues(head).strip()

        if len(value) > 1:
            value = value.lstrip('0')
        if len(value) == 0:
            value = "0"

        return self.createList(value)

    def doubleValues(self, node: Optional[ListNode]) -> int:
        result = "0"
        while node:
            double = node.val * 2
            result = result[:-1] + str(int(result[-1])+double//10) + str(double%10)
            node = node.next
        return result

    def createList(self, value: str) -> Optional[ListNode]:
        root = ListNode()
        node = root
        for index in range(len(value)):
            temp = ListNode(val=int(value[index]))
            node.next = temp
            node = temp

        return root.next
```
