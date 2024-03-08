![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Smallest Number In Infinite Set](https://leetcode.com/problems/smallest-number-in-infinite-set)

### Solution :

Method 1 :
```rust
use std::collections::HashSet;
struct SmallestInfiniteSet {
    popped: HashSet<i32>,
    minimum: i32,
}

/**
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl SmallestInfiniteSet {

    fn new() -> Self {
        Self {
            popped: HashSet::new(),
            minimum: 1,
        }
    }

    fn pop_smallest(&mut self) -> i32 {
        self.popped.insert(self.minimum);

        let result = self.minimum;
        for i in self.minimum..10000 {
        match self.popped.contains(&i) {
            true => (),
            false => {
                self.minimum = i;
                break;
            },
        };
        }

        result
    }

    fn add_back(&mut self, num: i32) {
        self.popped.remove(&num);

        if num < self.minimum {
            self.minimum = num;
        }
    }
}

/**
 * Your SmallestInfiniteSet object will be instantiated and called as such:
 * let obj = SmallestInfiniteSet::new();
 * let ret_1: i32 = obj.pop_smallest();
 * obj.add_back(num);
 */
```

Method 2 :
```rust
use std::collections::BTreeSet;
struct SmallestInfiniteSet {
    added: BTreeSet<i32>,
    minimum: i32,
}

/**
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl SmallestInfiniteSet {

    fn new() -> Self {
        Self {
            added: BTreeSet::new(),
            minimum: 1,
        }
    }

    fn pop_smallest(&mut self) -> i32 {
        match self.added.is_empty() {
            true => {
                self.minimum += 1;
                (self.minimum - 1)
            },
            false => {
                let &minimum_in_set = self.added.iter().next().unwrap();
                self.added.take(&minimum_in_set).unwrap()
            },
        }
    }

    fn add_back(&mut self, num: i32) {
        if num < self.minimum {
            self.added.insert(num);
        }
    }
}

/**
 * Your SmallestInfiniteSet object will be instantiated and called as such:
 * let obj = SmallestInfiniteSet::new();
 * let ret_1: i32 = obj.pop_smallest();
 * obj.add_back(num);
 */
```

Method 3 :
```rust
use std::collections::BTreeSet;
struct SmallestInfiniteSet {
    available: BTreeSet<i32>,
}

/**
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl SmallestInfiniteSet {

    fn new() -> Self {
        Self {
            available: BTreeSet::from([1]),
        }
    }

    fn pop_smallest(&mut self) -> i32 {
        let &minimum = self.available.iter().next().unwrap();

        self.available.remove(&minimum);
        if self.available.is_empty() {
            self.available.insert(minimum + 1);
        }

        minimum
    }

    fn add_back(&mut self, num: i32) {
        match self.available.iter().next_back() {
            Some(largest_available) => if largest_available > &num {
                self.available.insert(num);
            },
            None => (),
        }
    }
}

/**
 * Your SmallestInfiniteSet object will be instantiated and called as such:
 * let obj = SmallestInfiniteSet::new();
 * let ret_1: i32 = obj.pop_smallest();
 * obj.add_back(num);
 */
```
