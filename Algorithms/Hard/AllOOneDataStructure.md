![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 432. [All O`one Data Structure](https://leetcode.com/problems/all-oone-data-structure)

### Solution :

```rust
/**
 * Your AllOne object will be instantiated and called as such:
 * let obj = AllOne::new();
 * obj.inc(key);
 * obj.dec(key);
 * let ret_3: String = obj.get_max_key();
 * let ret_4: String = obj.get_min_key();
 */
```

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of total calls)) :
```rust
use std::collections::HashMap;

struct AllOne {
    counter: HashMap<String, i32>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl AllOne {

    fn new() -> Self {
        return Self {
            counter: Default::default(),
        }
    }

    fn inc(&mut self, key: String) {
        self.counter.entry(key.clone()).and_modify(|value| *value += 1).or_insert(1);
    }

    fn dec(&mut self, key: String) {
        self.counter.entry(key.clone()).and_modify(|value| *value -= 1).or_insert(0);

        if self.counter[&key] == 0 {
            self.counter.remove(&key);
        }
    }

    fn get_max_key(&self) -> String {
        if self.counter.len() == 0 {
            return "".to_string()
        }

        let mut amount: i32 = i32::MIN;
        let mut result: String = "".to_string();
        for (key, count) in self.counter.iter() {
            if *count > amount {
                amount = *count;
                result = key.clone();
            }
        }

        return result
    }

    fn get_min_key(&self) -> String {
        if self.counter.len() == 0 {
            return "".to_string()
        }

        let mut amount: i32 = i32::MAX;
        let mut result: String = "".to_string();
        for (key, count) in self.counter.iter() {
            if *count < amount {
                amount = *count;
                result = key.clone();
            }
        }

        return result
    }
}
```
