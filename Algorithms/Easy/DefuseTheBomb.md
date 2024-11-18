![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 1652. [Defuse The Bomb](https://leetcode.com/problems/defuse-the-bomb)

### Solution :

Method 1 (Time Complexity: $O(N*K)$, Space Complexity: $O(1)$ (N: the number of the elements in `code`, K: the value of `k`)) :
```rust
impl Solution {
    pub fn decrypt(code: Vec<i32>, k: i32) -> Vec<i32> {
        let n: usize = code.len();
        let mut result: Vec<i32> = vec![0; n];
        for index in 0..n {
            let mut sum: i32 = 0;
            for offset in 1..=k.abs() {
                if k < 0 {
                    sum += code[(n as i32+(index as i32 -offset)) as usize % n];
                } else {
                    sum += code[(index as i32 +offset) as usize % n];
                }
            }

            result[index] = sum;
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N*K)$, Space Complexity: $O(1)$ (N: the number of the elements in `code`, K: the value of `k`)) :
```java
class Solution {
    public int[] decrypt(int[] code, int k) {
        int n = code.length;
        int[] result = new int[n];
        for (int index=0; index<n; index++) {
            int sum = 0;
            for (int offset=1; offset<=Math.abs(k); offset++) {
                if (k < 0) {
                    sum += code[(n+index-offset)%n];
                } else {
                    sum += code[(index+offset)%n];
                }
            }

            result[index] = sum;
        }

        return result;
    }
}
```
