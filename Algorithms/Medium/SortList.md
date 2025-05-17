![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 148. [Sort List](https://leetcode.com/problems/sort-list)

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

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in the linked list)) :
```rust
impl Solution {
    pub fn sort_list(mut head: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
        let mut nums: Vec<i32> = Vec::new();
        Self::traverse_read(head.as_ref(), &mut nums);
        nums.sort();
        Self::traverse_update(head.as_mut(), 0, &nums);

        return head
    }

    fn traverse_read(node: Option<&Box<ListNode>>, nums: &mut Vec<i32>) {
        if node.is_none() {
            return
        } else if let Some(inner) = node {
            nums.push(inner.as_ref().val);
            Self::traverse_read(inner.next.as_ref(), nums);
        }
    }

    fn traverse_update(node: Option<&mut Box<ListNode>>, index: usize, nums: &Vec<i32>) {
        if node.is_none() {
            return
        } else if let Some(mut inner) = node {
            inner.as_mut().val = nums[index];
            Self::traverse_update(inner.next.as_mut(), index+1, nums);
            return
        }

        unreachable!();
    }
}
```
