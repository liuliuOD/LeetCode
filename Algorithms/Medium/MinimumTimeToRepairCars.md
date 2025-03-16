![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2594. [Minimum Time To Repair Cars](https://leetcode.com/problems/minimum-time-to-repair-cars)

### Solution :

Method 1 (AI by Grok3, Binary Search, Time Complexity: $O(N*Log(T))$, Space Complexity: $O(1)$ (N: the number of elements in `ranks`, T: the maximum possible time)) :
```rust
impl Solution {
    pub fn repair_cars(ranks: Vec<i32>, cars: i32) -> i64 {
        let cars = cars as i64;
        let mut left: i64 = 1;
        let mut right: i64 = i64::MAX; // Upper bound for time

        // Binary search on time
        while left < right {
            let mid = left + (right - left) / 2;

            // Calculate total cars that can be repaired in 'mid' time
            let total_cars: i64 = ranks.iter()
                .map(|&r| {
                    let r = r as i64;

                    // Number of cars = sqrt(mid / r)
                    return ((mid / r) as f64).sqrt() as i64
                })
                .sum();

            // If we can repair enough cars, try less time
            if total_cars >= cars {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left // Minimum time found
    }
}
```
