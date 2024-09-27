![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 731. [My Calendar II](https://leetcode.com/problems/my-calendar-ii)

### Solution :

```rust
/**
 * Your MyCalendarTwo object will be instantiated and called as such:
 * let obj = MyCalendarTwo::new();
 * let ret_1: bool = obj.book(start, end);
 */
```

Method 1 (Array, Time Complexity: $O(M*N+N^2)$, Space Complexity: $O(M+N)$ (M: the number of each overlapping event, N: the number of total call)) :
```rust
struct MyCalendarTwo {
    events: Vec<(i32, i32)>,
    overlapping: Vec<(i32, i32)>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl MyCalendarTwo {

    fn new() -> Self {
        return Self {
            events: Default::default(),
            overlapping: Default::default(),
        }
    }
    
    fn book(&mut self, start: i32, end: i32) -> bool {
        for &(start_overlapping, end_overlapping) in self.overlapping.iter() {
            if start < end_overlapping && start_overlapping < end {
                return false
            }
        }

        for &(start_previous, end_previous) in self.events.iter() {
            if start_previous < end && start < end_previous {
                self.overlapping.push((i32::max(start, start_previous), i32::min(end, end_previous)));
            }
        }

        self.events.push((start, end));
        return true
    }
}
```
