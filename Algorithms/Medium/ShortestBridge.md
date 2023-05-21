![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 934. [Shortest Bridge](https://leetcode.com/problems/shortest-bridge/)

### Solution :

Method 1 (DFS + BFS) :
```rust
use std::iter::FromIterator;
use std::collections::{ HashSet, VecDeque };
impl Solution {
    pub fn shortest_bridge(mut grid: Vec<Vec<i32>>) -> i32 {
        let moves: Vec<(i32, i32)> = vec![(1, 0), (-1, 0), (0, 1), (0, -1)];
        let start_point: (usize, usize) = Self::findStart(&grid);
        let mut start_water: HashSet<((usize, usize), i32)> = HashSet::new();
        Self::findStartWater(&mut start_water, &mut grid, &moves, start_point);
        return Self::findShortestBridge(&mut grid, &start_water, &moves)
    }

    // simple traverse
    fn findStart(grid: &Vec<Vec<i32>>) -> (usize, usize) {
        for i in 0..grid.len() {
            for j in 0..grid[0].len() {
                if grid[i][j] == 1 {
                    return (i, j)
                }
            }
        }

        return (0, 0)
    }

    // DFS
    fn findStartWater(start_water: &mut HashSet<((usize, usize), i32)>, grid: &mut Vec<Vec<i32>>, moves: &Vec<(i32, i32)>, start_point: (usize, usize)) {
        grid[start_point.0][start_point.1] = -1;
        for m in moves.iter() {
            let next_x = (start_point.0 as i32 + m.0) as usize;
            let next_y = (start_point.1 as i32 + m.1) as usize;
            if next_x >= grid.len() || next_y >= grid[0].len() {
                continue;
            }

            match grid[next_x][next_y] {
                0 => {
                    start_water.insert(((next_x, next_y), 0));
                },
                1 => Self::findStartWater(start_water, grid, moves, (next_x, next_y)),
                _ => (),
            }
        }
    }

    // BFS
    fn findShortestBridge(grid: &mut Vec<Vec<i32>>, start_water: &HashSet<((usize, usize), i32)>, moves: &Vec<(i32, i32)>) -> i32 {
        let mut queue: VecDeque<((usize, usize), i32)> = VecDeque::from_iter(start_water.into_iter().map(|&x| x).collect::<Vec<_>>());

        while !queue.is_empty() {
            let (point, value) = queue.pop_front().unwrap();

            for m in moves.iter() {
                let next_x = (point.0 as i32 + m.0) as usize;
                let next_y = (point.1 as i32 + m.1) as usize;
                if next_x >= grid.len() || next_y >= grid[0].len() {
                    continue;
                }

                match grid[next_x][next_y] {
                    0 => {
                        grid[next_x][next_y] = -1;
                        queue.push_back(((next_x, next_y), value + 1));
                    },
                    1 => {
                        return value + 1
                    },
                    _ => (),
                }
            }
        }

        return 0
    }
}
```

### Solution :

Method 1 (DFS + BFS) :
```python
class Solution:
    def shortestBridge(self, grid: List[List[int]]) -> int:
        self.moves = [(0, 1), (0, -1), (1, 0), (-1, 0)]
        self.grid = grid
        # in set => (step, i, j)
        self.start_water = set()
        start_i, start_j = self.findFirstLand(0, 0)
        self.findStartWaterSurroundFirstIsland(start_i, start_j)
        
        return self.findShortestBridge()

    def findFirstLand(self, start_i: int, start_j: int) -> (int, int):
        for i in range(start_i, len(self.grid)):
            for j in range(start_j, len(self.grid[0])):
                if self.grid[i][j] == 1:
                    return i, j

    def findStartWaterSurroundFirstIsland(self, i: int, j: int):
        # mark as visited
        self.grid[i][j] = -1

        for move_i, move_j in self.moves:
            next_i = i + move_i
            next_j = j + move_j
            if next_i < 0 or next_i >=len(self.grid) or next_j < 0 or next_j >= len(self.grid[0]):
                continue
            
            if self.grid[next_i][next_j] == 1:
                self.findStartWaterSurroundFirstIsland(next_i, next_j)
            elif self.grid[next_i][next_j] == 0:
                self.start_water.add((0, next_i, next_j))
    
    def findShortestBridge(self) -> int:
        queue = collections.deque(list(self.start_water))
        while queue:
            (start_step, start_i, start_j) = queue.popleft()

            for move_i, move_j in self.moves:
                next_i = start_i + move_i
                next_j = start_j + move_j
                if next_i < 0 or next_i >=len(self.grid) or next_j < 0 or next_j >= len(self.grid[0]):
                    continue
                
                if self.grid[next_i][next_j] == 1:
                    return start_step + 1
                elif self.grid[next_i][next_j] == 0:
                    self.grid[next_i][next_j] = -1
                    queue.append((start_step + 1, next_i, next_j))
```
