![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2349. [Design A Number Container System](https://leetcode.com/problems/design-a-number-container-system)

### Solution :

```rust
/**
 * Your NumberContainers object will be instantiated and called as such:
 * let obj = NumberContainers::new();
 * obj.change(index, number);
 * let ret_2: i32 = obj.find(number);
 */
```

Method 1 (Hash Map + Ordered Set, Time Complexity: $O(Log(N))$, Space Complexity: $O(N)$ (N: the number of indices and unique numbers)) :
```rust
use std::collections::{HashMap, BTreeSet};

struct NumberContainers {
    buckets: HashMap<i32, BTreeSet<i32>>,
    mapping: HashMap<i32, i32>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl NumberContainers {

    fn new() -> Self {
        return Self {
            buckets: HashMap::new(),
            mapping: HashMap::new(),
        }
    }

    fn change(&mut self, index: i32, number: i32) {
        if self.mapping.contains_key(&index) {
            let key_bucket: i32 = *self.mapping.get(&index).unwrap();
            self.buckets.entry(key_bucket).and_modify(|set| { set.remove(&index); });
        }

        self.mapping.entry(index).and_modify(|value| *value = number).or_insert(number);
        self.buckets.entry(number).and_modify(|set| { set.insert(index); }).or_insert(BTreeSet::from([index]));
    }

    fn find(&self, number: i32) -> i32 {
        if let Some(set) = self.buckets.get(&number) {
            if let Some(index) = set.first() {
                return *index
            }
        }

        return -1
    }
}
```
