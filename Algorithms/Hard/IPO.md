![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 502. [IPO](https://leetcode.com/problems/ipo)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```rust
use std::collections::BinaryHeap;

impl Solution {
    pub fn find_maximized_capital(k: i32, mut w: i32, profits: Vec<i32>, capital: Vec<i32>) -> i32 {
        let n: usize = profits.len();
        let mut projects: Vec<(i32, usize)> = vec![];
        for index in 0..n {
            projects.push((capital[index], index));
        }
        projects.sort();

        let mut result: i32 = 0;
        let mut index: usize = 0;
        let mut max_heap: BinaryHeap<i32> = BinaryHeap::new();
        for _ in 0..k {
            while index < n && projects[index].0 <= w {
                max_heap.push(profits[projects[index].1]);
                index += 1;
            }

            if max_heap.len() == 0 {
                break;
            }
            w += max_heap.pop().unwrap();
        }

        return w
    }
}
```

Method 2 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```rust
use std::collections::BinaryHeap;

struct Project {
    capital: i32,
    profit: i32,
}
impl Solution {
    pub fn find_maximized_capital(k: i32, mut w: i32, profits: Vec<i32>, capital: Vec<i32>) -> i32 {
        let n: usize = profits.len();
        let mut projects: Vec<Project> = profits.iter().zip(capital.iter()).map(|(&p, &c)| Project{capital: c, profit: p}).collect();
        projects.sort_unstable_by_key(|a| a.capital);

        let mut result: i32 = 0;
        let mut index: usize = 0;
        let mut max_heap: BinaryHeap<i32> = BinaryHeap::with_capacity(n);
        for _ in 0..k {
            while index < n && projects[index].capital <= w {
                max_heap.push(projects[index].profit);
                index += 1;
            }

            if max_heap.len() == 0 {
                break;
            }
            w += max_heap.pop().unwrap();
        }

        return w
    }
}
```

### Solution :

Method 1 (Hash Map + Binary Heap, Time Complexity: $O()$, Space Complexity: $O()$, ERROR: "Time Limit Exceeded", 32/35) :
```python
class Solution:
    def findMaximizedCapital(self, k: int, w: int, profits: List[int], capital: List[int]) -> int:
        n = len(profits)
        projects = defaultdict(list)
        for index in range(n):
            heapq.heappush(projects[capital[index]], -profits[index])

        capital = list(set(capital))
        capital.sort()
        for _ in range(k):
            key_projects = -1
            maximum = -inf

            for cost in capital:
                if cost > w:
                    break
                if -projects[cost][0] > maximum:
                    maximum = -projects[cost][0]
                    key_projects = cost

            if key_projects == -1:
                break

            heapq.heappop(projects[key_projects])
            if not projects[key_projects]:
                del projects[key_projects]
                capital.remove(key_projects)

            w += maximum

        return w
```

Method 2 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMaximizedCapital(self, k: int, w: int, profits: List[int], capital: List[int]) -> int:
        n = len(profits)
        # Option 1
        projects = [(capital[index], profits[index]) for index in range(n)]
        projects.sort()
        """
        # Option 2

        projects = sorted((capital[index], profits[index]) for index in range(n))
        """
        index = 0
        heap = []
        for _ in range(k):
            while index < n and projects[index][0] <= w:
                heapq.heappush(heap, -projects[index][1])
                index += 1

            if not heap:
                break

            w += -heapq.heappop(heap)

        return w
```
