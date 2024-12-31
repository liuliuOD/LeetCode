![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 983. [Minimum Cost For Tickets](https://leetcode.com/problems/minimum-cost-for-tickets)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `days`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn mincost_tickets(days: Vec<i32>, costs: Vec<i32>) -> i32 {
        let n: usize = days.len();
        let mut memoization: Vec<HashMap<i32, i32>> = vec![HashMap::new(); n];
        
        return Self::dfs(0, days[0]-1, &mut memoization, &days, &costs)
    }

    fn dfs(index_days: usize, maximum_day: i32, memoization: &mut Vec<HashMap<i32, i32>>, days: &Vec<i32>, costs: &Vec<i32>) -> i32 {
        let n: usize = days.len();
        if index_days >= n {
            return 0
        }

        if memoization[index_days].contains_key(&maximum_day) {
            return *memoization[index_days].get(&maximum_day).unwrap()
        }

        let mut minimum: i32 = i32::MAX;
        let index_next_days_1: usize = Self::get_next_index_days(index_days, maximum_day+1, days);
        // choose_1
        let mut cost_1: i32 = costs[0];
        if index_next_days_1 < n {
            cost_1 += Self::dfs(index_next_days_1, days[index_next_days_1]-1, memoization, days, costs);
        }
        minimum = i32::min(minimum, cost_1);

        let index_next_days_7: usize = Self::get_next_index_days(index_days, maximum_day+7, days);
        // choose_7
        let mut cost_7: i32 = costs[1];
        if index_next_days_7 < n {
            cost_7 += Self::dfs(index_next_days_7, days[index_next_days_7]-1, memoization, days, costs);
        }
        minimum = i32::min(minimum, cost_7);

        let index_next_days_30: usize = Self::get_next_index_days(index_days, maximum_day+30, days);
        // choose_30
        let mut cost_30: i32 = costs[2];
        if index_next_days_30 < n {
            cost_30 += Self::dfs(index_next_days_30, days[index_next_days_30]-1, memoization, days, costs);
        }
        minimum = i32::min(minimum, cost_30);

        memoization[index_days].entry(maximum_day).or_insert(minimum);
        return *memoization[index_days].get(&maximum_day).unwrap()
    }

    fn get_next_index_days(mut index_days: usize, maximum_day: i32, days: &Vec<i32>) -> usize {
        while index_days < days.len() && days[index_days] <= maximum_day {
            index_days += 1;
        }

        return index_days
    }
}
```
