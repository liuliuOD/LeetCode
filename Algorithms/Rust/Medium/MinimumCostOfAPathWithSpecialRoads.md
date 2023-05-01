## [Minimum Cost of a Path With Special Roads](https://leetcode.com/problems/minimum-cost-of-a-path-with-special-roads)

### Solution :

Method 1 (Dijkstra) :
```rust
use std::cmp;
use std::collections::{BinaryHeap, HashMap};
impl Solution {
    pub fn minimum_cost(start: Vec<i32>, target: Vec<i32>, special_roads: Vec<Vec<i32>>) -> i32 {
        let mut distances = HashMap::new();
        let mut special_points = vec![];

        for road in special_roads {
            let distance_normal = (road[0] - road[2]).abs() + (road[1] - road[3]).abs();
            if distance_normal > road[4] {
                special_points.push((road[0], road[1], road[2], road[3], road[4]));
            }
        }

        distances.insert((start[0], start[1]), 0);
        let mut heap = BinaryHeap::from([(cmp::Reverse(0), start[0], start[1])]);
        while !heap.is_empty() {
            if let Some((cmp::Reverse(cost), current_x, current_y)) = heap.pop() {
                for &(path_start_x, path_start_y, path_target_x, path_target_y, cost_target) in special_points.iter() {
                    let current_to_path_start = (current_x - path_start_x).abs() + (current_y - path_start_y).abs();
                    let cost_start_to_path_target = cost + current_to_path_start + cost_target;

                    if !distances.contains_key(&(path_target_x, path_target_y)) {
                        // initialize cost = start -> path_target
                        distances.insert((path_target_x, path_target_y), (start[0] - path_target_x).abs() + (start[1] - path_target_y).abs());
                    }

                    if cost_start_to_path_target < distances[&(path_target_x, path_target_y)] {
                        distances.insert((path_target_x, path_target_y), cost_start_to_path_target);
                        heap.push((cmp::Reverse(cost_start_to_path_target), path_target_x, path_target_y));
                    }
                }
            }
        }

        let mut result = i32::MAX;
        // don't need to calculate the cost from the start to the target because start position has been included in the distances
        for (distance, cost) in distances.iter() {
            result = cmp::min(result, cost + (target[0] - distance.0).abs() + (target[1] - distance.1).abs());
        }
        result
    }
}
```
