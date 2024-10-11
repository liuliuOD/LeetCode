![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1942. [The Number Of The Smallest Unoccupied Chair](https://leetcode.com/problems/the-number-of-the-smallest-unoccupied-chair)

### Solution :

Method 1 (Sorted, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of the elements in `times`)) :
```rust
impl Solution {
    pub fn smallest_chair(mut times: Vec<Vec<i32>>, target_friend: i32) -> i32 {
        let n: usize = times.len();
        let target_arrival_time: i32 = times[target_friend as usize][0];
        times.sort_by_key(|item| item[0]);
        let mut leaving_times: Vec<i32> = vec![0; n];
        for time in times {
            for index in 0..n {
                if leaving_times[index] > time[0] {
                    continue;
                }

                if time[0] == target_arrival_time {
                    return index as _
                }
                leaving_times[index] = time[1];
                break
            }
        }

        unreachable![];
    }
}
```
