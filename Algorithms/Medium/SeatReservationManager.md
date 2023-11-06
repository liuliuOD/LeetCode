![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1845. [Seat Reservation Manager](https://leetcode.com/problems/seat-reservation-manager)

```rust
/**
 * Your SeatManager object will be instantiated and called as such:
 * let obj = SeatManager::new(n);
 * let ret_1: i32 = obj.reserve();
 * obj.unreserve(seatNumber);
 */
```

### Solution :

Method 1 (Binary Search) :
```rust
struct SeatManager {
    seats: Vec<i32>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl SeatManager {

    fn new(n: i32) -> Self {
        Self {
            seats: (1..=n).rev().collect(),
        }
    }

    fn reserve(&mut self) -> i32 {
        return self.seats.pop().unwrap()
    }

    fn unreserve(&mut self, seat_number: i32) {
        let mut left: usize = 0;
        let mut right: usize = self.seats.len();
        while left < right {
            let middle: usize = left + (right - left) / 2;
            if self.seats[middle] < seat_number {
                right = middle;
            } else {
                left = middle + 1;
            }
        }

        self.seats.insert(left, seat_number);
    }
}
```

Method 2 (Binary Heap) :
```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;
struct SeatManager {
    seats: BinaryHeap<Reverse<i32>>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl SeatManager {

    fn new(n: i32) -> Self {
        /* Option 1 */
        let mut heap: BinaryHeap<Reverse<i32>> = BinaryHeap::new();
        for value in 1..=n {
            heap.push(Reverse(value));
        }
        Self {
            seats: heap,
        }
        /* Option 2

        Self {
            seats: BinaryHeap::from((1..=n).map(|value| Reverse(value)).collect::<Vec<Reverse<i32>>>()),
        }
        */
    }

    fn reserve(&mut self) -> i32 {
        /* Option 1 */
        return match self.seats.pop() {
            Some(Reverse(seat)) => seat,
            _ => 0,
        }
        /* Option 2

        return self.seats.pop().unwrap().0
        */
    }

    fn unreserve(&mut self, seat_number: i32) {
        self.seats.push(Reverse(seat_number));
    }
}
```

Method 3 (Binary Heap without default values) :
```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;
struct SeatManager {
    minimum: i32,
    seats: BinaryHeap<Reverse<i32>>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl SeatManager {

    fn new(n: i32) -> Self {
        Self {
            minimum: 1,
            seats: BinaryHeap::new(),
        }
    }

    fn reserve(&mut self) -> i32 {
        if self.seats.is_empty() {
            self.minimum += 1;
            return self.minimum - 1
        }

        return self.seats.pop().unwrap().0
    }

    fn unreserve(&mut self, seat_number: i32) {
        self.seats.push(Reverse(seat_number));
    }
}
```

### Solution :

```python
# Your SeatManager object will be instantiated and called as such:
# obj = SeatManager(n)
# param_1 = obj.reserve()
# obj.unreserve(seatNumber)
```

Method 1 (Binary Search, Time Complexity: $O(M*N)$ (M: the maximum number of calls made, N: value of `n`), Space Complexity: $O(N)$) :
```python
class SeatManager:

    def __init__(self, n: int):
        self.seats = list(range(n, 0, -1))

    def reserve(self) -> int:
        return self.seats.pop()

    def unreserve(self, seat_number: int) -> None:
        left = 0
        right = len(self.seats)
        while left < right:
            middle = left + (right-left)//2
            if self.seats[middle] < seat_number:
                right = middle
            else:
                left = middle + 1

        # In the worst case, it will have a time complexity of O(N)
        self.seats.insert(left, seat_number)
```

Method 2 (Binary Heap, Time Complexity: $O((M+N)*Log(N))$ (M: the maximum number of calls made, N: value of `n`), Space Complexity: $O(N)$) :
```python
class SeatManager:

    def __init__(self, n: int):
        self.heap = list(range(1, n+1))

    def reserve(self) -> int:
        return heapq.heappop(self.heap)

    def unreserve(self, seat_number: int) -> None:
        heapq.heappush(self.heap, seat_number)
```

Method 3 (Binary Heap without default values, Time Complexity: $O(M*Log(N))$ (M: the maximum number of calls made, N: value of `n`), Space Complexity: $O(N)$) :
```python
class SeatManager:

    def __init__(self, n: int):
        self.minimum = 1
        self.heap = []

    def reserve(self) -> int:
        if self.heap:
            return heapq.heappop(self.heap)

        self.minimum += 1
        return self.minimum - 1

    def unreserve(self, seat_number: int) -> None:
        heapq.heappush(self.heap, seat_number)
```
