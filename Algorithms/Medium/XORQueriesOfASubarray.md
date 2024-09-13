![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1310. [XOR Queries Of A Subarray](https://leetcode.com/problems/xor-queries-of-a-subarray)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(M+N)$, Space Complexity: $O(M)$ (M: the number of the elements in `arr`, N: the number of the elements in `queries`)) :
```rust
impl Solution {
    pub fn xor_queries(arr: Vec<i32>, queries: Vec<Vec<i32>>) -> Vec<i32> {
        let n: usize = arr.len();
        let mut prefix_xor: Vec<i32> = Vec::with_capacity(n+1);
        prefix_xor.push(0);
        for element in arr {
            prefix_xor.push(prefix_xor.last().unwrap()^element);
        }

        let m: usize = queries.len();
        let mut result: Vec<i32> = Vec::with_capacity(m);
        for query in queries {
            result.push(prefix_xor[(query[1] as usize)+1]^prefix_xor[query[0] as usize]);
        }

        return result
    }
}
```

Method 2 (Prefix Sum, Time Complexity: $O(M+N)$, Space Complexity: $O(1)$ (M: the number of the elements in `arr`, N: the number of the elements in `queries`)) :
```rust
impl Solution {
    pub fn xor_queries(mut arr: Vec<i32>, queries: Vec<Vec<i32>>) -> Vec<i32> {
        let n: usize = arr.len();
        for index in 1..n {
            arr[index] ^= arr[index-1];
        }

        let m: usize = queries.len();
        let mut result: Vec<i32> = Vec::with_capacity(m);
        for query in queries {
            if query[0] == 0 {
                result.push(arr[query[1] as usize]);
            } else {
                result.push(arr[query[1] as usize]^arr[(query[0] as usize)-1]);
            }
        }

        return result
    }
}
```
