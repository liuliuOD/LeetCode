![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 705. [Design Hash Set](https://leetcode.com/problems/design-hashset)

### Solution :

```rust
/**
 * Your MyHashSet object will be instantiated and called as such:
 * let obj = MyHashSet::new();
 * obj.add(key);
 * obj.remove(key);
 * let ret_3: bool = obj.contains(key);
 */
```

Method 1 (Array) :
```rust
const SET_LENGTH:usize = 10_usize.pow(6) + 1;
struct MyHashSet {
    set: [bool; SET_LENGTH],
}

impl MyHashSet {

    fn new() -> Self {
        Self {
            set: [false; SET_LENGTH],
        }
    }
    
    fn add(&mut self, key: i32) {
        self.set[key as usize] = true;
    }
    
    fn remove(&mut self, key: i32) {
        self.set[key as usize] = false;
    }
    
    fn contains(&self, key: i32) -> bool {
        return self.set[key as usize]
    }
}
```

### Solution :

```python
# Your MyHashSet object will be instantiated and called as such:
# obj = MyHashSet()
# obj.add(key)
# obj.remove(key)
# param_3 = obj.contains(key)
```

Method 1 (Linked List) :
```python
class MyHashSet:

    def __init__(self):
        self.head = ListNode(val=None)
        self.tail = self.head

    def add(self, key: int) -> None:
        if self.contains(key):
            return
        self.tail.next = ListNode(val=key)
        self.tail = self.tail.next

    def remove(self, key: int) -> None:
        node = self.head
        while node:
            if node.next and node.next.val == key:
                node.next = node.next.next
                if node.next == None:
                    self.tail = node
                break
            node = node.next

    def contains(self, key: int) -> bool:
        node = self.head
        while node:
            if node.val == key:
                return True
            node = node.next
        return False
        
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```
