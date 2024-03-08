![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Dota2 Senate](https://leetcode.com/problems/dota2-senate)

### Solution :

Method 1 (Single Queue) :
```rust
use std::cmp::Ordering;
use std::collections::VecDeque;
impl Solution {
    pub fn predict_party_victory(senate: String) -> String {
        let mut queue = VecDeque::new();
        for (index, player) in senate.chars().into_iter().enumerate() {
            match player {
                'R' => queue.push_back('R'),
                'D' => queue.push_back('D'),
                _ => (),
            };
        }

        let mut amount_R = 0;
        let mut amount_D = 0;
        let stop_amount = queue.len();
        // set amount limit to prevent infinite loop
        while !queue.is_empty() && amount_R < stop_amount && amount_D < stop_amount {
            let senate = queue.pop_front().unwrap();
            match senate {
                'R' => {
                    if amount_D > 0 {
                        amount_D -= 1;
                    } else {
                        amount_R += 1;
                        queue.push_back('R');
                    }
                },
                'D' => {
                    if amount_R > 0 {
                        amount_R -= 1;
                    } else {
                        amount_D += 1;
                        queue.push_back('D');
                    }
                },
                _ => (),
            }
        }

        let result_R = "Radiant".to_string();
        let result_D = "Dire".to_string();
        match amount_R.cmp(&amount_D) {
            Ordering::Greater => result_R,
            Ordering::Less | Ordering::Equal => result_D,
        }
    }
}
```

Method 2 (Double Queue) :
```rust
use std::cmp::Ordering;
use std::collections::VecDeque;
impl Solution {
    pub fn predict_party_victory(senate: String) -> String {
        let mut queue_R = VecDeque::new();
        let mut queue_D = VecDeque::new();
        for (index, role) in senate.chars().into_iter().enumerate() {
            if role == 'R' {
                queue_R.push_back(index);
            } else {
                queue_D.push_back(index);
            }
        }

        let n = senate.len();
        while !queue_R.is_empty() && !queue_D.is_empty() {
            let index_R = queue_R.pop_front().unwrap();
            let index_D = queue_D.pop_front().unwrap();

            match index_R.cmp(&index_D) {
                Ordering::Greater => queue_D.push_back(index_D + n),
                Ordering::Less => queue_R.push_back(index_R + n),
                _ => (),
            }
        }

        if queue_R.is_empty() {
            return "Dire".to_string()
        }

        "Radiant".to_string()
    }
}
```
