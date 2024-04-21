![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 1992. [Find All Groups Of Farmland](https://leetcode.com/problems/find-all-groups-of-farmland)

### Solution :

Method 1 (Greedy, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn find_farmland(mut land: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
        let mut result: Vec<Vec<i32>> = vec![];
        let m: usize = land.len();
        let n: usize = land[0].len();
        for r1 in 0..m {
            for c1 in 0..n {
                if land[r1][c1] == 0 {
                    continue;
                }

                let mut r2: usize = r1;
                let mut c2: usize = c1;
                while r2 < m && land[r2][c1] == 1 {
                    c2 = c1;
                    while c2 < n && land[r2][c2] == 1 {
                        land[r2][c2] = 0;
                        c2 += 1;
                    }
                    r2 += 1;
                }

                result.push(vec![r1 as i32, c1 as i32, (r2 as i32)-1, (c2 as i32)-1]);
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (DFS, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$) :
```python
class Solution:
    def findFarmland(self, land: List[List[int]]) -> List[List[int]]:
        m = len(land)
        n = len(land[0])
        result = []
        for index_m in range(m):
            for index_n in range(n):
                if land[index_m][index_n] == 0:
                    continue
                land[index_m][index_n] = 0

                r1, c1 = index_m, index_n
                r2, c2 = r1, c1
                stack = [(r1, c1)]
                while stack:
                    rm, cn = stack.pop()
                    for offset_m, offset_n in [(0, 1), (1, 0)]:
                        index_m_next, index_n_next = rm + offset_m, cn + offset_n
                        if index_m_next >= m or index_n_next >= n or land[index_m_next][index_n_next] == 0:
                            continue
                        land[index_m_next][index_n_next] = 0

                        stack.append((index_m_next, index_n_next))
                        if index_m_next >= r2 and index_n_next >= c2:
                            r2, c2 = index_m_next, index_n_next

                result.append([r1, c1, r2, c2])

        return result
```

Method 2 (BFS, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$) :
```python
class Solution:
    def findFarmland(self, land: List[List[int]]) -> List[List[int]]:
        m = len(land)
        n = len(land[0])
        result = []
        for index_m in range(m):
            for index_n in range(n):
                if land[index_m][index_n] == 0:
                    continue
                land[index_m][index_n] = 0

                r1, c1 = index_m, index_n
                r2, c2 = r1, c1
                queue = deque([(r1, c1)])
                while queue:
                    rm, cn = queue.popleft()
                    for offset_m, offset_n in [(0, 1), (1, 0)]:
                        index_m_next, index_n_next = rm + offset_m, cn + offset_n
                        if index_m_next >= m or index_n_next >= n or land[index_m_next][index_n_next] == 0:
                            continue
                        land[index_m_next][index_n_next] = 0

                        queue.append((index_m_next, index_n_next))
                        if index_m_next >= r2 and index_n_next >= c2:
                            r2, c2 = index_m_next, index_n_next

                result.append([r1, c1, r2, c2])

        return result
```

Method 3 (Greedy, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findFarmland(self, land: List[List[int]]) -> List[List[int]]:
        m = len(land)
        n = len(land[0])
        result = []
        for index_m in range(m):
            for index_n in range(n):
                if land[index_m][index_n] == 0:
                    continue

                r1, c1 = index_m, index_n
                r2, c2 = r1, c1
                while r2 < m and land[r2][c1] == 1:
                    c2 = c1
                    while c2 < n and land[r2][c2] == 1:
                        land[r2][c2] = 0
                        c2 += 1
                    r2 += 1

                result.append([r1, c1, r2-1, c2-1])

        return result
```

### Solution :

Method 1 (Greedy, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$) :
```go
func findFarmland(land [][]int) [][]int {
    var result [][]int
    m := len(land)
    n := len(land[0])
    for r1 := 0; r1 < m; r1++ {
        for c1 := 0; c1 < n; c1++ {
            if land[r1][c1] == 0 {
                continue
            }

            r2 := r1
            c2 := c1
            for ; r2 < m && land[r2][c1] == 1; r2++ {
                c2 = c1
                for ; c2 < n && land[r2][c2] == 1; c2++ {
                    land[r2][c2] = 0;
                }
            }

            result = append(result, []int{r1, c1, r2-1, c2-1})
        }
    }

    return result
}
```
