![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 514. [Freedom Trail](https://leetcode.com/problems/freedom-trail)

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(M^2*N)$ (M: length of `ring`, N: length of `key`), Space Complexity: $O(M)$) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn find_rotate_steps(ring: String, key: String) -> i32 {
        let ring: Vec<u8> = ring.bytes().collect::<Vec<u8>>();
        let key: Vec<u8> = key.bytes().collect::<Vec<u8>>();
        let m: i32 = ring.len() as i32;
        let n: i32 = key.len() as i32;
        let mut mapping: HashMap<u8, Vec<i32>> = HashMap::new();
        for (index, &ascii) in ring.iter().enumerate() {
            mapping.entry(ascii).or_default().push(index as i32);
        }

        let mut dp: Vec<i32> = vec![i32::MAX; m as usize];
        dp[0] = 0;
        for index_n in 0..n {
            let mut temp: Vec<i32> = vec![i32::MAX; m as usize];
            for &index_m in mapping.get(&key[index_n as usize]).unwrap() {
                for (index_previous, &moves) in dp.iter().enumerate() {
                    if moves == i32::MAX {
                        continue;
                    }

                    temp[index_m as usize] = temp[index_m as usize].min(1 + moves + (index_m-index_previous as i32).abs().min((m-(index_m-index_previous as i32).abs())));
                }
            }

            dp = temp;
        }

        return *dp.iter().min().unwrap()
    }
}
```

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(M*N)$ (M: length of `ring`, N: length of `key`), Space Complexity: $O(M*N)$) :
```python
class Solution:
    def findRotateSteps(self, ring: str, key: str) -> int:
        return min(self.dfs(0, 0, 1, ring, key), self.dfs(0, 0, -1, ring, key))

    @cache
    def dfs(self, index_ring: int, index_key: int, direction: int, ring: str, key: str) -> int:
        n_ring = len(ring)
        if index_ring < 0:
            index_ring = n_ring - 1
        elif index_ring >= n_ring:
            index_ring = 0

        if index_key >= len(key):
            return 0

        result = inf
        if ring[index_ring] == key[index_key]:
            result = min(result, 1 + self.dfs(index_ring, index_key+1, direction, ring, key), 1 + self.dfs(index_ring, index_key+1, -direction, ring, key))
        else:
            result = min(result, 1 + self.dfs(index_ring+direction, index_key, direction, ring, key))

        return result
```

Method 2 (DFS + Memoization, Time Complexity: $O(M*N)$ (M: length of `ring`, N: length of `key`), Space Complexity: $O(M*N)$) :
```python
class Solution:
    def findRotateSteps(self, ring: str, key: str) -> int:
        n_ring = len(ring)

        @cache
        def dfs(index_ring: int, index_key: int, direction: int) -> int:
            if index_ring < 0:
                index_ring = n_ring - 1
            elif index_ring >= n_ring:
                index_ring = 0

            if index_key >= len(key):
                return 0

            result = inf
            if ring[index_ring] == key[index_key]:
                result = min(result, 1 + dfs(index_ring, index_key+1, direction), 1 + dfs(index_ring, index_key+1, -direction))
            else:
                result = min(result, 1 + dfs(index_ring+direction, index_key, direction))

            return result

        return min(dfs(0, 0, 1), dfs(0, 0, -1))
```

Method 3 (DFS + Memoization, Time Complexity: $O(M*N)$ (M: length of `ring`, N: length of `key`), Space Complexity: $O(M*N)$) :
```python
class Solution:
    def findRotateSteps(self, ring: str, key: str) -> int:
        n_ring = len(ring)

        memoization = {}
        def dfs(index_ring: int, index_key: int, direction: int) -> int:
            key_m = (index_ring, index_key, direction)
            if key_m in memoization:
                return memoization[key_m]

            if index_ring < 0:
                index_ring = n_ring - 1
            elif index_ring >= n_ring:
                index_ring = 0

            if index_key >= len(key):
                return 0

            result = inf
            if ring[index_ring] == key[index_key]:
                result = min(result, 1 + dfs(index_ring, index_key+1, direction), 1 + dfs(index_ring, index_key+1, -direction))
            else:
                result = min(result, 1 + dfs(index_ring+direction, index_key, direction))

            memoization[key_m] = result
            return result

        return min(dfs(0, 0, 1), dfs(0, 0, -1))
```

Method 4 (Dynamic Programming, Time Complexity: $O(M^2*N)$ (M: length of `ring`, N: length of `key`), Space Complexity: $O(M)$) :
```python
class Solution:
    def findRotateSteps(self, ring: str, key: str) -> int:
        m = len(ring)
        n = len(key)
        mapping = defaultdict(list)
        for index, char in enumerate(ring):
            mapping[char].append(index)

        dp = [inf] * m
        dp[0] = 0
        for index_n in range(n):
            temp = [inf] * m
            for index_m in mapping[key[index_n]]:
                for index_previous, move in enumerate(dp):
                    # inf means we can't be there
                    if move is inf:
                        continue

                    temp[index_m] = min(temp[index_m], 1 + move + min(abs(index_m-index_previous), m-abs(index_m-index_previous)))

            dp = temp

        return min(dp)
```
