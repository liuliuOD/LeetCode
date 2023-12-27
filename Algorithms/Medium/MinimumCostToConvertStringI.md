![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2976. [Minimum Cost To Convert String I](https://leetcode.com/problems/minimum-cost-to-convert-string-i)

### Solution :

Method 1 (Floyd Warshall) :
```rust
const BASE: u8 = 'a' as u8;
impl Solution {
    pub fn minimum_cost(source: String, target: String, original: Vec<char>, changed: Vec<char>, cost: Vec<i32>) -> i64 {
        let mut graph: [[i64; 26]; 26] = [[i64::MAX; 26]; 26];
        for index in 0..original.len() {
            let start: usize = (original[index] as u8 - BASE) as usize;
            let target: usize = (changed[index] as u8 - BASE) as usize;
            graph[start][target] = graph[start][target].min(cost[index] as i64);
        }

        Self::floyd_warshall(&mut graph);

        let mut result: i64 = 0;
        for (s, t) in source.as_bytes().iter().zip(target.as_bytes().iter()) {
            if s == t {
                continue;
            }

            let start: usize = (s - BASE) as usize;
            let target: usize = (t - BASE) as usize;
            if graph[start][target] == i64::MAX {
                return -1
            }

            result += graph[start][target];
        }

        return result
    }

    fn floyd_warshall(graph: &mut [[i64; 26]; 26]) {
        let n: usize = 26;
        for index_pivot in 0..n {
            for index_start in 0..n {
                for index_target in 0..n {
                    if graph[index_start][index_pivot] == i64::MAX || graph[index_pivot][index_target] == i64::MAX {
                        continue;
                    }

                    let cost: i64 = graph[index_start][index_pivot] + graph[index_pivot][index_target];
                    if graph[index_start][index_target] <= cost {
                        continue;
                    }

                    graph[index_start][index_target] = cost;
                }
            }
        }
    }
}
```

### Solution :

Method 1 (BFS, Time Complexity: $O(MAX(26*26, N))$ (N: length of `source`), Space Complexity: $O(1)$) :
```python
CARDINALITY = 26
BASE = ord('a')
class Solution:
    def minimumCost(self, source: str, target: str, original: List[str], changed: List[str], cost: List[int]) -> int:
        graph = defaultdict(list)
        for index in range(len(original)):
            graph[ord(original[index])-BASE].append((ord(changed[index])-BASE, cost[index]))

        costs: List[List[int]] = [[inf]*CARDINALITY for _ in range(CARDINALITY)]
        for index in range(CARDINALITY):
            self.bfs(index, costs, graph)

        result = 0
        for index in range(len(source)):
            if source[index] == target[index]:
                continue

            cost_current = costs[ord(source[index])-BASE][ord(target[index])-BASE]
            if cost_current is inf:
                return -1

            result += cost_current

        return result

    def bfs(self, start: int, costs: List[List[int]], graph: Dict[int, List[int]]):
        queue = deque([(start, 0)])
        while queue:
            current, cost = queue.popleft()
            for after, cost_after in graph[current]:
                cost_accumulation = cost + cost_after
                if costs[start][after] <= cost_accumulation:
                    continue

                costs[start][after] = cost_accumulation
                queue.append((after, cost_accumulation))
```

Method 2 (BFS + Binary Heap) :
```python
CARDINALITY = 26
BASE = ord('a')
class Solution:
    def minimumCost(self, source: str, target: str, original: List[str], changed: List[str], cost: List[int]) -> int:
        graph = defaultdict(list)
        for index in range(len(original)):
            graph[ord(original[index])-BASE].append((ord(changed[index])-BASE, cost[index]))

        costs: List[List[int]] = [[inf]*CARDINALITY for _ in range(CARDINALITY)]
        for index in range(CARDINALITY):
            self.bfs(index, costs, graph)

        result = 0
        for index in range(len(source)):
            if source[index] == target[index]:
                continue

            cost_current = costs[ord(source[index])-BASE][ord(target[index])-BASE]
            if cost_current is inf:
                return -1

            result += cost_current

        return result

    def bfs(self, start: int, costs: List[List[int]], graph: Dict[int, List[int]]):
        heap = [(0, start)]
        while heap:
            cost, current = heapq.heappop(heap)
            for after, cost_after in graph[current]:
                cost_accumulation = cost + cost_after
                if costs[start][after] <= cost_accumulation:
                    continue

                costs[start][after] = cost_accumulation
                heapq.heappush(heap, (cost_accumulation, after))
```

Method 3 (Floyd Warshall, Time Complexity: $O(M^3)$ (M: length of `original`), Space Complexity: $O(1)$) :
```python
CARDINALITY = 26
BASE = ord('a')
class Solution:
    def minimumCost(self, source: str, target: str, original: List[str], changed: List[str], cost: List[int]) -> int:
        costs: List[List[int]] = [[inf]*CARDINALITY for _ in range(CARDINALITY)]
        for index in range(len(original)):
            costs[ord(original[index])-BASE][ord(changed[index])-BASE] = min(costs[ord(original[index])-BASE][ord(changed[index])-BASE], cost[index])

        self.floydWarshall(costs)

        result = 0
        for index in range(len(source)):
            if source[index] == target[index]:
                continue

            cost_current = costs[ord(source[index])-BASE][ord(target[index])-BASE]
            if cost_current is inf:
                return -1

            result += cost_current

        return result

    def floydWarshall(self, costs: List[List[int]]):
        for index_pivot in range(CARDINALITY):
            for index_start in range(CARDINALITY):
                for index_target in range(CARDINALITY):
                    cost_pivot = costs[index_start][index_pivot] + costs[index_pivot][index_target]
                    if costs[index_start][index_target] <= cost_pivot:
                        continue

                    costs[index_start][index_target] = cost_pivot
```
