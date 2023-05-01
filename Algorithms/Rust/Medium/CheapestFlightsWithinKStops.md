## [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops)

### Solution :

Method 1 (Dijkstra) :
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
