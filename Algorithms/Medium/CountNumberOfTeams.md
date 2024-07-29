![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1395. [Count Number Of Teams](https://leetcode.com/problems/count-number-of-teams)

### Solution :

Method 1 (Brute Force, Time Complexity: $(N^3)$, Space Complexity: $O(1)$ (N: numbers of the elements in `rating`)) :
```rust
impl Solution {
    pub fn num_teams(rating: Vec<i32>) -> i32 {
        let n: usize = rating.len();
        let mut result: i32 = 0;
        for index_first in 0..n-2 {
            let rate_first: i32 = rating[index_first];
            for index_second in index_first+1..n-1 {
                let rate_second: i32 = rating[index_second];
                for index_third in index_second+1..n {
                    let rate_third: i32 = rating[index_third];
                    if (rate_first > rate_second && rate_second > rate_third) || (rate_first < rate_second && rate_second < rate_third) {
                        result += 1;
                    }
                }
            }
        }

        return result
    }
}
```

Method 2 (Dynamic Programming, Time Complexity: $(N^2)$, Space Complexity: $O(N)$ (N: numbers of the elements in `rating`)) :
```rust
impl Solution {
    pub fn num_teams(rating: Vec<i32>) -> i32 {
        let n: usize = rating.len();
        let mut counter_increase: Vec<i32> = Vec::with_capacity(n);
        let mut counter_decrease: Vec<i32> = Vec::with_capacity(n);
        for index_current in 0..n {
            if index_current == 0 || index_current == n-1 {
                counter_increase.push(0);
                counter_decrease.push(0);
                continue
            }

            let current: i32 = rating[index_current];
            let mut amount_increase: i32 = 0;
            let mut amount_decrease: i32 = 0;
            for index_start in 0..index_current {
                if rating[index_start] > current {
                    amount_decrease += 1;
                }
                if rating[index_start] < current {
                    amount_increase += 1;
                }
            }

            counter_increase.push(amount_increase);
            counter_decrease.push(amount_decrease);
        }

        let mut result: i32 = 0;
        for index_current in 0..n {
            if counter_increase[index_current] == 0 && counter_decrease[index_current] == 0 {
                continue
            }

            let current: i32 = rating[index_current];
            for index_next in index_current+1..n {
                if counter_increase[index_current] > 0 && current < rating[index_next] {
                    result += counter_increase[index_current];
                }
                if counter_decrease[index_current] > 0 && current > rating[index_next] {
                    result += counter_decrease[index_current];
                }
            }
        }

        return result
    }
}
```

Method 3 (Dynamic Programming + Optimization, Time Complexity: $(N^2)$, Space Complexity: $O(1)$ (N: numbers of the elements in `rating`)) :
```rust
impl Solution {
    pub fn num_teams(rating: Vec<i32>) -> i32 {
        let n: usize = rating.len();
        let mut result: i32 = 0;
        for index_current in 1..n-1 {
            let current: i32 = rating[index_current];
            let mut amount_increase: i32 = 0;
            let mut amount_decrease: i32 = 0;
            for index_start in 0..index_current {
                if rating[index_start] > current {
                    amount_decrease += 1;
                }
                if rating[index_start] < current {
                    amount_increase += 1;
                }
            }

            if amount_increase == 0 && amount_decrease == 0 {
                continue
            }

            for index_next in index_current+1..n {
                if amount_increase > 0 && current < rating[index_next] {
                    result += amount_increase;
                }
                if amount_decrease > 0 && current > rating[index_next] {
                    result += amount_decrease;
                }
            }
        }

        return result
    }
}
```
