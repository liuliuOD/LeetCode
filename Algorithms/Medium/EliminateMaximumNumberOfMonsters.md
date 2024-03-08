![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1921. [Eliminate Maximum Number Of Monsters](https://leetcode.com/problems/eliminate-maximum-number-of-monsters)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn eliminate_maximum(dist: Vec<i32>, speed: Vec<i32>) -> i32 {
        let mut times: Vec<i32> = dist.iter().zip(speed.iter()).map(|(d, s)| (d+s-1) / s).collect();
        times.sort();

        let mut result: i32 = 0;
        for time in times {
            if time <= result {
                break;
            }

            result += 1;
        }

        return result
    }
}
```

Method 2 (Counting Sort) :
```rust
impl Solution {
    pub fn eliminate_maximum(dist: Vec<i32>, speed: Vec<i32>) -> i32 {
        let n: usize = dist.len();
        let times: Vec<usize> = dist.iter().zip(speed.iter()).map(|(d, s)| ((d+s-1) / s) as usize).collect();
        let mut counting_sort: Vec<i32> = vec![0; n];
        for time in times {
            if time >= n {
                continue;
            }

            counting_sort[time] += 1;
        }

        let mut result: i32 = 1;
        for index in 1..n {
            counting_sort[index] += counting_sort[index-1];
            if counting_sort[index] > result {
                break;
            }

            result += 1;
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def eliminateMaximum(self, dist: List[int], speed: List[int]) -> int:
        # ceil
        time_to_arrive = [(d+s-1) // s for d, s in zip(dist, speed)]
        time_to_arrive.sort()
        result = 0
        for time in time_to_arrive:
            if time <= result:
                break

            result += 1

        return result
```

Method 2 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def eliminateMaximum(self, dist: List[int], speed: List[int]) -> int:
        # ceil
        time_to_arrive = [(d+s-1) // s for d, s in zip(dist, speed)]
        heapq.heapify(time_to_arrive)
        result = 0
        while time_to_arrive:
            if heapq.heappop(time_to_arrive) <= result:
                break

            result += 1

        return result
```

Method 3 (Counting Sort, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def eliminateMaximum(self, dist: List[int], speed: List[int]) -> int:
        n = len(dist)
        time_to_arrive = [(d+s-1) // s for d, s in zip(dist, speed)]

        counting_sort = [0] * n
        for time in time_to_arrive:
            if time >= n:
                continue

            counting_sort[time] += 1

        result = 1
        for index in range(1, n):
            # Prefix Sum
            counting_sort[index] += counting_sort[index-1]
            if counting_sort[index] > result:
                break

            result += 1

        return result
```
