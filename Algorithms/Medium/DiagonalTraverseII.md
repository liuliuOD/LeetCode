![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1424. [Diagonal Traverse II](https://leetcode.com/problems/diagonal-traverse-ii)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn find_diagonal_order(nums: Vec<Vec<i32>>) -> Vec<i32> {
        let mut result: Vec<(usize, i32, i32)> = vec![];
        for index_x in 0..nums.len() {
            for index_y in 0..nums[index_x].len() {
                result.push((index_x+index_y, -(index_x as i32), nums[index_x][index_y]));
            }
        }

        result.sort();
        return result.iter().map(|item| item.2).collect()
    }
}
```

Method 2 (BFS) :
```rust
use std::collections::VecDeque;

impl Solution {
    pub fn find_diagonal_order(nums: Vec<Vec<i32>>) -> Vec<i32> {
        let mut result: Vec<i32> = vec![];
        let mut queue: VecDeque<(usize, usize)> = VecDeque::from([(0, 0)]);
        while !queue.is_empty() {
            let (x, y) = queue.pop_front().unwrap();

            result.push(nums[x][y]);

            if y == 0 && x+1 < nums.len() {
                queue.push_back((x+1, y));
            }
            if y+1 < nums[x].len() {
                queue.push_back((x, y+1));
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (ERROR: "Time Limit Exceeded", 53/56) :
```python
class Solution:
    def findDiagonalOrder(self, nums: List[List[int]]) -> List[int]:
        result = []
        n = len(nums)
        # Option 1
        for index_x in range(n):
            for index_y in range(len(nums[index_x])):
                index_result = index_x + index_y
                target = nums[index_x][index_y]
                if len(result) > index_result:
                    result[index_result].append(target)
                else:
                    result.append([target])

        return reduce(lambda a, b: a + b[::-1], result, [])
        """
        # Option 2

        maximum_y = max([len(group) for group in nums])
        # maximum_y = max(nums, key=len)
        for index_y in range(maximum_y):
            for index_x in range(n):
                if index_y >= len(nums[index_x]):
                    continue

                target = nums[index_x][index_y]
                if len(result) > index_result:
                    result[index_result].append(target)
                else:
                    result.append([target])

        return reduce(lambda a, b: a + b, result, [])
        """
```

Method 2 :
```python
class Solution:
    def findDiagonalOrder(self, nums: List[List[int]]) -> List[int]:
        result = []
        n = len(nums)
        for index_x in range(n):
            for index_y in range(len(nums[index_x])):
                index_result = index_x + index_y
                target = nums[index_x][index_y]
                result.append((index_result, -index_x, target))

        return map(lambda item: item[2], sorted(result))
```

Method 3 :
```python
class Solution:
    def findDiagonalOrder(self, nums: List[List[int]]) -> List[int]:
        n = len(nums)
        groups = defaultdict(list)
        for index_x in reversed(range(n)):
            for index_y in range(len(nums[index_x])):
                groups[index_x+index_y].append(nums[index_x][index_y])

        result = []
        index = 0
        while index in groups:
            result.extend(groups[index])

            index += 1

        return result
```

Method 4 (BFS, Time Complexity: $O(N)$ (N: amount of items in `nums`), Space Complexity: O($\sqrt{N}$)) :
```python
class Solution:
    def findDiagonalOrder(self, nums: List[List[int]]) -> List[int]:
        result = []
        queue = deque([(0, 0)])
        while queue:
            x, y = queue.popleft()
            result.append(nums[x][y])
            if y == 0 and x+1 < len(nums):
                queue.append((x+1, y))

            if y+1 < len(nums[x]):
                queue.append((x, y+1))

        return result
```
