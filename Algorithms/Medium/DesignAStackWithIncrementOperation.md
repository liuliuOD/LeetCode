![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1381. [Design A Stack With Increment Operation](https://leetcode.com/problems/design-a-stack-with-increment-operation)

### Solution :

```rust
/**
 * Your CustomStack object will be instantiated and called as such:
 * let obj = CustomStack::new(maxSize);
 * obj.push(x);
 * let ret_2: i32 = obj.pop();
 * obj.increment(k, val);
 */
```

Method 1 (Array, Time Complexity: $O(N)$, Space Complexity: $O(M)$ (M: the value of `maxSize`, N: the number of total calls)) :
```rust
struct CustomStack {
    maximum: usize,
    items: Vec<i32>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl CustomStack {

    fn new(maxSize: i32) -> Self {
        return Self {
            maximum: maxSize as usize,
            items: Default::default(),
        }
    }

    fn push(&mut self, x: i32) {
        if self.items.len() >= self.maximum {
            return
        }

        self.items.push(x);
    }

    fn pop(&mut self) -> i32 {
        return match self.items.pop() {
            Some(value) => value,
            None => -1,
        }
    }

    fn increment(&mut self, k: i32, val: i32) {
        for index in 0..usize::min(k as usize, self.items.len()) {
            self.items[index] += val;
        }
    }
}
```
