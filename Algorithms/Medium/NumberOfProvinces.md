![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 547. [Number Of Provinces](https://leetcode.com/problems/number-of-provinces)

### Solution :

Method 1 (DFS) :
```rust
use std::collections::{HashMap, HashSet};
impl Solution {
    pub fn find_circle_num(is_connected: Vec<Vec<i32>>) -> i32 {
        let n = is_connected.len();
        let mut adjust_list: HashMap<usize, Vec<usize>> = HashMap::new();
        for i in 0..n {
            for j in 0..n {
                if i == j || is_connected[i][j] != 1 {
                    continue;
                }
                adjust_list.entry(i).or_default().push(j);
            }
        }

        let mut result = n as i32;
        let mut visited: HashSet<usize> = HashSet::new();
        for (&key, _) in adjust_list.iter() {
            if visited.contains(&key) {
                continue;
            }
            result = result - Self::dfs(key, &adjust_list, &mut visited) + 1;
        }

        return result
    }

    fn dfs(key: usize, adjust_list: &HashMap<usize, Vec<usize>>, visited: &mut HashSet<usize>) -> i32 {
        if visited.contains(&key) {
            return 0
        }
        visited.insert(key);

        let mut amount: i32 = 0;
        for &index_conntected in adjust_list[&key].iter() {
            amount += Self::dfs(index_conntected, adjust_list, visited);
        }

        return amount + 1
    }
}
```

### Solution :

Method 1 (DFS) :
```python
class Solution:
    def findCircleNum(self, isConnected: List[List[int]]) -> int:
        n = len(isConnected)
        self.adjust_list = defaultdict(list)
        for i in range(n):
            for j in range(n):
                if i is not j and isConnected[i][j] == 1:
                    self.adjust_list[i].append(j)
        
        result = n
        self.visited = [False for _ in range(n)]
        for key, adjust in self.adjust_list.items():
            if self.visited[key]:
                continue
            result = result - self.dfs(key) + 1
        return result
    
    def dfs(self, index: int) -> int:
        if self.visited[index]:
            return 0
        self.visited[index] = True

        amount = 0
        for index_connected in self.adjust_list[index]:
            amount += self.dfs(index_connected)
        return amount + 1
```
