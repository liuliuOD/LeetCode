![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1290. [Convert Binary Number In A Linked List To Integer](https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer)

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

Method 1 (Vector) :
```rust
impl Solution {
    pub fn get_decimal_value(head: Option<Box<ListNode>>) -> i32 {
        let mut binary = vec![];
        let mut node = head;
        while let Some(temp) = node {
            binary.push(temp.val);
            node = temp.next;
        }

        return binary.iter().fold(0, |acc, digit| (acc << 1) | digit)
    }
}
```

Method 2 (binary to decimal) :
```rust
impl Solution {
    pub fn get_decimal_value(head: Option<Box<ListNode>>) -> i32 {
        let mut decimal: i32 = 0;
        let mut node = head;
        while let Some(temp) = node {
            decimal <<= 1;
            decimal |= temp.val;
            node = temp.next;
        }

        return decimal
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

Method 1 (list + join) :
```python
class Solution:
    def getDecimalValue(self, head: ListNode) -> int:
        binary_list = []
        while head:
            binary_list.append(head.val)
            head = head.next
        return int(''.join(map(str, binary_list)), 2)
```

Method 2 (string) :
```python
class Solution:
    def getDecimalValue(self, head: ListNode) -> int:
        binary_string = ''
        while head:
            binary_string += str(head.val)
            head = head.next
        return int(binary_string, 2)
```
