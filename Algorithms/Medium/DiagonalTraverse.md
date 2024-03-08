![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 498. [Diagonal Traverse](https://leetcode.com/problems/diagonal-traverse)

### Solution :

Method 1 :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn find_diagonal_order(mat: Vec<Vec<i32>>) -> Vec<i32> {
        let mut mapping: HashMap<usize, Vec<i32>> = HashMap::new();
        for index_x in 0..mat.len() {
            for index_y in 0..mat[index_x].len() {
                mapping.entry(index_x+index_y).and_modify(|group| group.push(mat[index_x][index_y])).or_insert(vec![mat[index_x][index_y]]);
            }
        }

        let mut result: Vec<i32> = vec![];
        let mut index: usize = 0;
        while mapping.contains_key(&index) {
            /* Option 1 */
            match index%2 {
                0 => result.extend(mapping[&index].iter().rev()),
                _ => result.extend(mapping[&index].clone()),
            };
            /* Option 2

            result.extend(match index%2 {
                0 => mapping[&index].iter().rev().map(|&item| item).collect(),
                _ => mapping[&index].clone(),
            });
            */

            index += 1;
        }

        return result
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn find_diagonal_order(mat: Vec<Vec<i32>>) -> Vec<i32> {
        let x: usize = mat.len();
        let y: usize = mat[0].len();
        let mut x_current: usize = 0;
        let mut y_current: usize = 0;
        let mut result: Vec<i32> = vec![];
        while (x_current+1)*(y_current+1) <= x*y {
            let mut x_temp: usize = x_current;
            let mut y_temp: usize = y_current;
            let mut temp: Vec<i32> = vec![];
            loop {
                temp.push(mat[x_temp][y_temp]);

                x_temp += 1;
                y_temp -= 1;
                if x_temp >= x || y_temp >= y {
                    break;
                }
            }

            if (x_current+y_current)%2 == 0 {
                temp.reverse();
            }

            /* Option 1 */
            result.extend(temp);
            /* Option 2

            result.extend(&temp);
            */
            /* Option 3

            result.append(&mut temp);
            */

            if y_current < y-1 {
                y_current += 1;
                x_current = 0;
            } else {
                x_current += 1;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def findDiagonalOrder(self, mat: List[List[int]]) -> List[int]:
        mapping = defaultdict(list)
        for index_x in range(len(mat)):
            for index_y in range(len(mat[index_x])):
                mapping[index_x+index_y].append(mat[index_x][index_y])

        result = []
        index = 0
        while index in mapping:
            result.extend(mapping[index][::-1] if index % 2 == 0 else mapping[index])
            index += 1

        return result
```

Method 2 (Stack) :
```python
class Solution:
    def findDiagonalOrder(self, mat: List[List[int]]) -> List[int]:
        result = [mat[0][0]]
        direction = True
        stack = [(0, 0)]
        while stack:
            amount = len(stack)
            temp = []
            for _ in range(amount):
                x, y = stack.pop()
                if direction:
                    if x == 0 and y+1 < len(mat[x]):
                        result.append(mat[x][y+1])
                        temp.append((x, y+1))
                    if x+1 < len(mat):
                        result.append(mat[x+1][y])
                        temp.append((x+1, y))
                else:
                    if y == 0 and x+1 < len(mat):
                        result.append(mat[x+1][y])
                        temp.append((x+1, y))
                    if y+1 < len(mat[x]):
                        result.append(mat[x][y+1])
                        temp.append((x, y+1))

            stack.extend(temp)

            direction = not direction

        return result
```

Method 3 (Queue) :
```python
class Solution:
    def findDiagonalOrder(self, mat: List[List[int]]) -> List[int]:
        result = [mat[0][0]]
        direction = True
        queue = deque([(0, 0)])
        while queue:
            amount = len(queue)
            for _ in range(amount):
                if direction:
                    x, y = queue.pop()
                    if x == 0 and y+1 < len(mat[x]):
                        result.append(mat[x][y+1])
                        queue.appendleft((x, y+1))
                    if x+1 < len(mat):
                        result.append(mat[x+1][y])
                        queue.appendleft((x+1, y))
                else:
                    x, y = queue.popleft()
                    if y == 0 and x+1 < len(mat):
                        result.append(mat[x+1][y])
                        queue.append((x+1, y))
                    if y+1 < len(mat[x]):
                        result.append(mat[x][y+1])
                        queue.append((x, y+1))

            direction = not direction

        return result
```
