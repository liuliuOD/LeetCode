## [Network Delay Time](https://leetcode.com/problems/network-delay-time)

### Solution :

Method 1 (Dijkstra) :
```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;
impl Solution {
    pub fn network_delay_time(times: Vec<Vec<i32>>, n: i32, k: i32) -> i32 {
        let mut distances = vec![i32::MAX; (n+1) as usize];
        let mut graph = vec![vec![]; (n+1) as usize ];
        for time in times {
            graph[time[0] as usize].push((time[1] as usize, time[2]));
        }

        distances[0] = 0;
        distances[k as usize] = 0;
        let mut heap = BinaryHeap::from([(Reverse(0), k as usize)]);
        while !heap.is_empty() {
            if let Some((Reverse(time), point)) = heap.pop() {
                for &(target_point, target_time) in graph[point].iter() {
                    let time_from_k_to_target = time + target_time;

                    if distances[target_point] > time_from_k_to_target {
                        distances[target_point] = time_from_k_to_target;
                        heap.push((Reverse(time_from_k_to_target), target_point));
                    }
                }
            }
        }

        match distances.iter().max() {
            Some(value) if *value < i32::MAX => *value,
            Some(value) if *value == i32::MAX => -1,
            _ => -1,
        }
    }
}
```
