![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 729. [My Calendar I](https://leetcode.com/problems/my-calendar-i)

### Solution :

```rust
/**
 * Your MyCalendar object will be instantiated and called as such:
 * let obj = MyCalendar::new();
 * let ret_1: bool = obj.book(start, end);
 */
```

Method 1 (Hash Set, ERROR: "Time Limit Exceeded", 95/107) :
```rust
use std::collections::HashSet;

struct MyCalendar {
    booked: HashSet<i32>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl MyCalendar {

    fn new() -> Self {
        return Self {
            booked: HashSet::new(),
        }
    }

    fn book(&mut self, start: i32, end: i32) -> bool {
        for current in start..end {
            if self.booked.contains(&current) {
                return false
            }
        }

        for current in start..end {
            self.booked.insert(current);
        }

        return true
    }
}
```

Method 2 (Array, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of total call)) :
```rust
struct MyCalendar {
    booked: Vec<(i32, i32)>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl MyCalendar {

    fn new() -> Self {
        return Self {
            booked: Vec::new(),
        }
    }

    fn book(&mut self, start: i32, end: i32) -> bool {
        for &(start_booked, end_booked) in self.booked.iter() {
            /* Option 1 */
            if (start_booked <= start && start < end_booked) || (start_booked < end && end < end_booked) || (start <= start_booked && start_booked < end) {
            /* Option 2
            if start_booked < end && start < end_booked {
            */
                return false
            }
        }

        self.booked.push((start, end));
        return true
    }
}
```
