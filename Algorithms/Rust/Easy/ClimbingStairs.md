## [Climbing Stairs](https://leetcode.com/problems/climbing-stairs)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded") :
```rust
impl Solution {
    pub fn climb_stairs(n: i32) -> i32 {
        match n {
            0 | 1 => 1,
            value => Self::climb_stairs(n - 1) + Self::climb_stairs(n - 2),
        }
    }
}
```

Method 2 (Dynamic Programming) :
```rust
use std::collections::HashMap;
impl Solution {
    
    pub fn climb_stairs(n: i32) -> i32 {
        let mut hm = HashMap::from([(0, 1), (1, 1)]);

        Self::dynamic_programming(n, &mut hm)
    }

    fn dynamic_programming(n: i32, hm: &mut HashMap<i32, i32>) -> i32 {
        match hm.get(&n) {
            Some(&value) => value,
            None => {
                let sum = Self::dynamic_programming(n - 1, hm) + Self::dynamic_programming(n - 2, hm);
                hm.insert(n, sum);

                return *hm.get(&n).unwrap()
            },
        }
    }
}
```
