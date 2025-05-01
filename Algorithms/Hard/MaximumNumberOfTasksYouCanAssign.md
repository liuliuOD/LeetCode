![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2071. [Maximum Number Of Tasks You Can Assign](https://leetcode.com/problems/maximum-number-of-tasks-you-can-assign)

### Solution :

Method 1 (AI by Grok3, Sorted Map + Binary Search, Time Complexity: $O(M*Log(M)+N*Log(N)+MIN(M, N)*Log(MIN(M, N))^2)$, Space Complexity: $O(Log(M)+Log(N)+MIN(M, N))$ (M: the number of the elements in `workers`, N: the number of the elements in `tasks`)) :
```rust
use std::collections::BTreeMap;

impl Solution {
    pub fn max_task_assign(tasks: Vec<i32>, workers: Vec<i32>, pills: i32, strength: i32) -> i32 {
        let mut tasks = tasks;
        let mut workers = workers;
        let n = tasks.len();
        let m = workers.len();

        // Sort tasks and workers
        tasks.sort();
        workers.sort();

        // Binary search for the maximum number of tasks that can be assigned
        let mut left = 1;
        let mut right = m.min(n) as i32;
        let mut ans = 0;
        while left <= right {
            let mid = (left + right) / 2;
            if Self::check(mid, &tasks, &workers, pills, strength) {
                ans = mid;
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return ans
    }

    fn check(mid: i32, tasks: &Vec<i32>, workers: &Vec<i32>, mut pills: i32, strength: i32) -> bool {
        let mid = mid as usize;
        let m = workers.len();

        // Create a BTreeMap to store worker strengths and their counts
        let mut ws: BTreeMap<i32, i32> = BTreeMap::new();
        for &w in workers.iter().skip(m - mid) {
            *ws.entry(w).or_insert(0) += 1;
        }

        // Process each task from largest to smallest
        for i in (0..mid).rev() {
            let task = tasks[i];

            // Find the largest worker strength
            if let Some((&max_strength, &count)) = ws.last_key_value() {
                if max_strength >= task {
                    // Use this worker
                    if count == 1 {
                        ws.remove(&max_strength);
                    } else {
                        *ws.get_mut(&max_strength).unwrap() -= 1;
                    }
                    continue;
                }
            }

            // If no worker is strong enough, try using a pill
            if pills == 0 {
                return false;
            }

            // Find the smallest worker who can handle the task with a pill
            let required_strength = task - strength;
            let mut found = false;
            for (&worker_strength, &count) in ws.range(required_strength..) {
                found = true;
                pills -= 1;
                if ws[&worker_strength] == 1 {
                    ws.remove(&worker_strength);
                } else {
                    *ws.get_mut(&worker_strength).unwrap() -= 1;
                }
                break;
            }

            if !found {
                return false;
            }
        }

        return true
    }
}
```
