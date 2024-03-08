![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Frequency Tracker](https://leetcode.com/problems/frequency-tracker)

### Solution :

Method 1 :
```rust
use std::collections::HashMap;
use std::collections::HashSet;
struct FrequencyTracker {
    numbers: HashMap<i32, i32>,
    frequency: HashMap<i32, HashSet<i32>>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl FrequencyTracker {

    fn new() -> Self {
        Self {
            numbers: HashMap::new(),
            frequency: HashMap::new(),
        }
    }
    
    fn add(&mut self, number: i32) {
        self.numbers.entry(number).or_insert(0);
        let mut times = self.numbers.get_mut(&number).unwrap();
        if *times > 0 {
            (*self.frequency.get_mut(times).unwrap()).remove(&number);
        }

        *times += 1;
        self.frequency.entry(*times).or_insert(HashSet::new());
        self.frequency.get_mut(times).unwrap().insert(number);
    }
    
    fn delete_one(&mut self, number: i32) {
        self.numbers.entry(number).or_insert(0);
        let mut times = self.numbers.get_mut(&number).unwrap();
        if *times <= 0 {
            return ()
        }

        (*self.frequency.get_mut(times).unwrap()).remove(&number);

        *times -= 1;
        self.frequency.entry(*times).or_insert(HashSet::new());
        self.frequency.get_mut(times).unwrap().insert(number);
    }
    
    fn has_frequency(&self, frequency: i32) -> bool {
        self.frequency.contains_key(&frequency) && (*self.frequency.get(&frequency).unwrap()).len() > 0
    }
}

/**
 * Your FrequencyTracker object will be instantiated and called as such:
 * let obj = FrequencyTracker::new();
 * obj.add(number);
 * obj.delete_one(number);
 * let ret_3: bool = obj.has_frequency(frequency);
 */
```
