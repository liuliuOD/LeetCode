![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2807. [Insert Greatest Common Divisors In Linked List](https://leetcode.com/problems/insert-greatest-common-divisors-in-linked-list)

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

Method 1 (Recursive GCD, Time Complexity: $O(M*Log(N))$, Space Complexity: $O(Log(N))$ (M: the number of the elements in the linked list, N: the averageof the elements' value in the linked list)) :
```rust
type Custom = Box<ListNode>;

impl Solution {
    pub fn insert_greatest_common_divisors(mut head: Option<Custom>) -> Option<Custom> {
        let mut current: &mut Custom = head.as_mut().unwrap();
        while current.next.is_some() {
            let a: i32 = i32::max(current.val, current.next.as_ref().unwrap().val);
            let b: i32 = i32::min(current.val, current.next.as_ref().unwrap().val);
            let mut node: ListNode = ListNode::new(Self::find_greatest_common_divisor(a, b));
            node.next = current.next.take();
            current.next = Some(Box::new(node));
            current = current.next.as_mut().unwrap().next.as_mut().unwrap();
        }

        return head
    }

    fn find_greatest_common_divisor(a: i32, b: i32) -> i32 {
        if b == 0 {
            return a
        }

        return Self::find_greatest_common_divisor(b, a%b)
    }
}
```
