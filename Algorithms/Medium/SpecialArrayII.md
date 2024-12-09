![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3152. [Special Array II](https://leetcode.com/problems/special-array-ii)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(M+N)$, Space Complexity: $O(N)$ (M: the number of the elements in `queries`, N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn is_array_special(nums: Vec<i32>, queries: Vec<Vec<i32>>) -> Vec<bool> {
        let n: usize = nums.len();
        let mut prefix_sum: Vec<i32> = vec![1];
        for index in 1..n {
            let mut current: i32 = prefix_sum[index-1];
            if nums[index]%2 != nums[index-1]%2 {
                current += 1;
            }
            prefix_sum.push(current);
        }

        let mut result: Vec<bool> = vec![];
        for query in queries.iter() {
            let current: bool = prefix_sum[query[1] as usize]-prefix_sum[query[0] as usize] == query[1]-query[0];

            result.push(current);
        }

        return result
    }
}
```

Method 2 (Prefix Sum, Time Complexity: $O(M+N)$, Space Complexity: $O(N)$ (M: the number of the elements in `queries`, N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn is_array_special(nums: Vec<i32>, queries: Vec<Vec<i32>>) -> Vec<bool> {
        let n: usize = nums.len();
        let mut counter: Vec<i32> = Vec::with_capacity(n);
        counter.push(0);
        for index in 1..n {
            if nums[index]%2 == nums[index-1]%2 {
                counter.push(*counter.last().unwrap() + 1);
            } else {
                counter.push(*counter.last().unwrap());
            }
        }

        let mut result: Vec<bool> = Vec::with_capacity(n);
        for query in queries {
            if counter[query[1] as usize]-counter[query[0] as usize] == 0 {
                result.push(true);
            } else {
                result.push(false);
            }
        }

        return result
    }
}
```

Method 3 (Prefix Sum, Time Complexity: $O(M+N)$, Space Complexity: $O(N)$ (M: the number of the elements in `queries`, N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn is_array_special(nums: Vec<i32>, queries: Vec<Vec<i32>>) -> Vec<bool> {
        let n: usize = nums.len();
        let mut current: i32 = 0;
        let mut counter: Vec<i32> = Vec::with_capacity(n);
        counter.push(current);
        for index in 1..n {
            if nums[index]%2 == nums[index-1]%2 {
                current += 1;
            }

            counter.push(current);
        }

        let mut result: Vec<bool> = Vec::with_capacity(n);
        for query in queries {
            result.push(counter[query[1] as usize]-counter[query[0] as usize] == 0);
        }

        return result
    }
}
```

### Solution :

Method 1 (In weekly contest 398, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def isArraySpecial(self, nums: List[int], queries: List[List[int]]) -> List[bool]:
        n = len(queries)
        queries_sort = sorted(enumerate(queries), key=lambda query: query[1])
        result = [False] * n
        index_start = 0
        index_end = 0
        is_special = True
        for index, query in queries_sort:
            if query[0] != index_start:
                index_start = index_end = query[0]
                is_special = True

            while index_end < query[1]:
                index_end += 1
                if nums[index_end]%2 == nums[index_end-1]%2:
                    is_special = False
                    break

            result[index] = is_special
        return result
```

Method 2 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def isArraySpecial(self, nums: List[int], queries: List[List[int]]) -> List[bool]:
        n = len(nums)
        prefix_sum = [1]
        for index in range(1, n):
            current = prefix_sum[-1]
            if nums[index]%2 != nums[index-1]%2:
                current += 1
            prefix_sum.append(current)

        result = []
        for index_start, index_end in queries:
            result.append(True if prefix_sum[index_end] - prefix_sum[index_start] == index_end-index_start else False)

        return result
```
