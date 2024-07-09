![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1701. [Average Waiting Time](https://leetcode.com/problems/average-waiting-time)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: number of the elements in `customers`)) :
```rust
impl Solution {
    pub fn average_waiting_time(customers: Vec<Vec<i32>>) -> f64 {
        let n: usize = customers.len();
        let mut time_current: i64 = customers[0][0] as i64;
        let mut time_waiting: i64 = 0;
        for customer in customers {
            let time_start: i64 = customer[0] as i64;
            let time_cost: i64 = customer[1] as i64;
            if time_start > time_current {
                time_current = time_start;
            }
            time_current += time_cost;
            time_waiting += time_current - time_start;
        }

        return time_waiting as f64 / n as f64
    }
}
```
