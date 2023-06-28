![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Path With Maximum Probability](https://leetcode.com/problems/path-with-maximum-probability)

### Solution :

Method 1 (Dijkstra, to prevent float and overflow, use i64 to store probability) :
```rust
use std::collections::BinaryHeap;
impl Solution {
    pub fn max_probability(n: i32, edges: Vec<Vec<i32>>, succ_prob: Vec<f64>, start: i32, end: i32) -> f64 {
        let baseline:i64 = 10_i64.pow(6);
        let mut graph = vec![vec![]; n as usize];
        for (edge, mut prob) in edges.iter().zip(succ_prob.iter()) {
            let prob = (*prob * baseline as f64) as i64;
            graph[edge[0] as usize].push((edge[1] as usize, prob));
            graph[edge[1] as usize].push((edge[0] as usize, prob));
        }

        let mut probability = vec![i64::MIN; n as usize];
        probability[start as usize] = 0;
        let mut heap = BinaryHeap::from([(baseline, start as usize)]);
        while !heap.is_empty() {
            let (prob_from, point_from) = heap.pop().unwrap();
            for &(point_to, prob_to) in graph[point_from].iter() {
                let prob_from_to = prob_from * prob_to / baseline;

                if prob_from_to > probability[point_to] {
                    probability[point_to] = prob_from_to;
                    heap.push((prob_from_to, point_to));
                }
            }
        }

        match probability[end as usize] {
            i64::MIN => 0.0,
            value => (value as f64) / baseline as f64,
        }
    }
}
```

Method 2 (BFS) :
```rust
use std::collections::VecDeque;
impl Solution {
    pub fn max_probability(n: i32, edges: Vec<Vec<i32>>, succ_prob: Vec<f64>, start: i32, end: i32) -> f64 {
        let mut graph = vec![vec![]; n as usize];
        for (edge, mut prob) in edges.iter().zip(succ_prob.iter()) {
            graph[edge[0] as usize].push((edge[1] as usize, prob));
            graph[edge[1] as usize].push((edge[0] as usize, prob));
        }

        let mut probability = vec![f64::MIN; n as usize];
        probability[start as usize] = 0.0;
        let mut queue = VecDeque::from([(1.0, start as usize)]);
        while !queue.is_empty() {
            let (prob_from, point_from) = queue.pop_front().unwrap();
            for &(point_to, prob_to) in graph[point_from].iter() {
                let prob_from_to = prob_from * prob_to;

                if prob_from_to > probability[point_to] {
                    probability[point_to] = prob_from_to;
                    queue.push_back((prob_from_to, point_to));
                }
            }
        }

        match probability[end as usize] {
            f64::MIN => 0.0,
            value => value,
        }
    }
}
```

### Solution :

Method 1 (Dijkstra) :
```python
class Solution:
    def maxProbability(self, n: int, edges: List[List[int]], succProb: List[float], start: int, end: int) -> float:
        self.mapping = defaultdict(list)
        for edge, prob in zip(edges, succProb):
            self.mapping[edge[0]].append((edge[1], prob))
            self.mapping[edge[1]].append((edge[0], prob))

        maximum_prob = defaultdict(int)
        maximum_prob[start] = 1
        heap = [(-1, start)]
        while heap:
            current_prob, current_node = heapq.heappop(heap)
            current_prob *= -1

            if current_node == end:
                return current_prob

            for target_node, target_prob in self.mapping[current_node]:
                current_to_target_prob = current_prob * target_prob
                if maximum_prob[target_node] >= current_to_target_prob:
                    continue
                maximum_prob[target_node] = current_to_target_prob
                heapq.heappush(heap, (-current_to_target_prob, target_node))
        return 0.0
```
