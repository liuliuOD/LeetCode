![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops)

### Solution :

Method 1 (Dijkstra, source to destination) :
```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;
impl Solution {
    pub fn find_cheapest_price(n: i32, flights: Vec<Vec<i32>>, src: i32, dst: i32, k: i32) -> i32 {
        let mut graph = vec![vec![]; n as usize];
        for flight in flights.iter() {
            graph[flight[0] as usize].push((flight[1] as usize, flight[2]));
        }

        let mut stop_times = vec![i32::MAX; n as usize];
        let mut heap = BinaryHeap::from([(Reverse(0), src as usize, 0)]);
        while !heap.is_empty() {
            let (Reverse(price), from, stops) = heap.pop().unwrap();

            if stops > k + 1 || stops > stop_times[from] {
                continue;
            }
            stop_times[from] = stops;

            if from == dst as usize {
                return price
            }

            for &(to, price_target) in graph[from].iter() {
                let price_from_src_to_target = price + price_target;

                heap.push((Reverse(price_from_src_to_target), to, stops + 1));
            }
        }

        -1
    }
}
```

Method 2 (Dijkstra, destination to source) :
```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;
impl Solution {
    pub fn find_cheapest_price(n: i32, flights: Vec<Vec<i32>>, src: i32, dst: i32, k: i32) -> i32 {
        let mut graph = vec![vec![]; n as usize];
        for flight in flights.iter() {
            graph[flight[1] as usize].push((flight[0] as usize, flight[2]));
        }

        let mut result : Vec<i32> = vec![i32::MAX; graph.len()];
        let mut heap = BinaryHeap::from([(Reverse(0), dst as usize, 0)]);
        while !heap.is_empty() {
            let (Reverse(price), to, stops) = heap.pop().unwrap();

            if stops > k + 1 {
                continue;
            }
            result[to] = price;

            if to == src as usize {
                break;
            }

            for &(from, price_target) in graph[to].iter() {
                let price_from_src_to_target = price + price_target;

                heap.push((Reverse(price_from_src_to_target), from, stops + 1));
            }
        }

        match result[src as usize] == i32::MAX {
            true => -1,
            false => result[src as usize],
        }
    }
}
```

Method 3 (BFS (ERROR: "Time Limit Exceeded")) :
```rust
use std::cmp;
use std::collections::VecDeque;
impl Solution {
    pub fn find_cheapest_price(n: i32, flights: Vec<Vec<i32>>, src: i32, dst: i32, k: i32) -> i32 {
        let mut graph = vec![vec![]; n as usize];
        for flight in flights.iter() {
            graph[flight[0] as usize].push((flight[1] as usize, flight[2]));
        }

        let mut result = i32::MAX;
        let mut queue = VecDeque::from([(0, src as usize, 0)]);
        while !queue.is_empty() {
            let (price, from, stops) = queue.pop_front().unwrap();

            for &(to, price_target) in graph[from].iter() {
                let price_from_src_to_target = price + price_target;

                if to == dst as usize {
                    result = cmp::min(result, price_from_src_to_target);
                    continue;
                }

                if stops >= k || price_from_src_to_target >= result {
                    continue;
                }
                queue.push_back((price_from_src_to_target, to, stops + 1));
            }
        }

        match result == i32::MAX {
            true => -1,
            false => result,
        }
    }
}
```

Method 4 (BFS, add limitation to prune execution times) :
```rust
use std::cmp;
use std::collections::VecDeque;
impl Solution {
    pub fn find_cheapest_price(n: i32, flights: Vec<Vec<i32>>, src: i32, dst: i32, k: i32) -> i32 {
        let mut graph = vec![vec![]; n as usize];
        for flight in flights.iter() {
            graph[flight[0] as usize].push((flight[1] as usize, flight[2]));
        }

        let mut result = i32::MAX;
        let mut prices = vec![i32::MAX; n as usize]; // use to reduce the nodes push into queue
        let mut queue = VecDeque::from([(0, src as usize, 0)]);
        while !queue.is_empty() {
            let (price, from, stops) = queue.pop_front().unwrap();

            for &(to, price_target) in graph[from].iter() {
                let price_from_src_to_target = price + price_target;

                if to == dst as usize {
                    result = cmp::min(result, price_from_src_to_target);
                    continue;
                }

                if stops >= k || price_from_src_to_target >= result || prices[to] <= price_from_src_to_target {
                    continue;
                }

                prices[to] = price_from_src_to_target;
                queue.push_back((price_from_src_to_target, to, stops + 1));
            }
        }

        match result == i32::MAX {
            true => -1,
            false => result,
        }
    }
}
```
