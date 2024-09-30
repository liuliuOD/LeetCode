![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 641. [Design Circular Deque](https://leetcode.com/problems/design-circular-deque)

### Solution :

```rust
/**
 * Your MyCircularDeque object will be instantiated and called as such:
 * let obj = MyCircularDeque::new(k);
 * let ret_1: bool = obj.insert_front(value);
 * let ret_2: bool = obj.insert_last(value);
 * let ret_3: bool = obj.delete_front();
 * let ret_4: bool = obj.delete_last();
 * let ret_5: i32 = obj.get_front();
 * let ret_6: i32 = obj.get_rear();
 * let ret_7: bool = obj.is_empty();
 * let ret_8: bool = obj.is_full();
 */
```

Method 1 (Linked List, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of total calls)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;

type Custom = Option<Rc<RefCell<Node>>>;

struct Node {
    value: i32,
    previous: Custom,
    next: Custom,
}

struct MyCircularDeque {
    capacity: i32,
    amount: i32,
    first: Custom,
    last: Custom,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl MyCircularDeque {

    fn new(k: i32) -> Self {
        return Self {
            capacity: k,
            amount: Default::default(),
            first: Default::default(),
            last: Default::default(),
        }
    }

    fn insert_front(&mut self, value: i32) -> bool {
        if self.amount >= self.capacity {
            return false
        }

        let node: Node = Node{value: value, next: self.first.clone(), previous: None};
        let item: Custom = Some(Rc::new(RefCell::new(node)));
        if self.first.is_some() {
            self.first.as_ref().unwrap().borrow_mut().previous = item.clone();
        }
        self.first = item.clone();
        if self.last.is_none() {
            self.last = item.clone();
        }
        self.amount += 1;

        return true
    }

    fn insert_last(&mut self, value: i32) -> bool {
        if self.amount >= self.capacity {
            return false
        }

        let node: Node = Node{value: value, previous: self.last.clone(), next: None};
        let item: Custom = Some(Rc::new(RefCell::new(node)));
        if self.last.is_some() {
            self.last.as_ref().unwrap().borrow_mut().next = item.clone();
        }
        self.last = item.clone();
        if self.first.is_none() {
            self.first = item.clone();
        }
        self.amount += 1;

        return true
    }

    fn delete_front(&mut self) -> bool {
        if self.amount == 0 {
            return false
        }
        else if self.amount == 1 {
            self.first = None;
            self.last = None;
        }
        else {
            let node_next: Custom = self.first.as_ref().unwrap().borrow().next.clone();
            self.first = node_next;
            if self.first.is_some() {
                self.first.as_ref().unwrap().borrow_mut().previous = None;
            }
        }

        self.amount -= 1;
        return true
    }

    fn delete_last(&mut self) -> bool {
        if self.amount == 0 {
            return false
        }
        else if self.amount == 1 {
            self.first = None;
            self.last = None;
        }
        else {
            let node_previous: Custom = self.last.as_ref().unwrap().borrow().previous.clone();
            self.last = node_previous;
            if self.last.is_some() {
                self.last.as_ref().unwrap().borrow_mut().next = None;
            }
        }

        self.amount -= 1;
        return true
    }

    fn get_front(&self) -> i32 {
        if self.first.is_none() {
            return -1
        }

        return self.first.as_ref().unwrap().borrow().value
    }
    
    fn get_rear(&self) -> i32 {
        if self.last.is_none() {
            return -1
        }

        return self.last.as_ref().unwrap().borrow().value
    }

    fn is_empty(&self) -> bool {
        return self.first.is_none()
    }

    fn is_full(&self) -> bool {
        return self.amount == self.capacity
    }
}
```
