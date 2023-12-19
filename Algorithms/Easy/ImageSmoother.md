![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 661. [Image Smoother](https://leetcode.com/problems/image-smoother)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn image_smoother(img: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
        let m: usize = img.len();
        let n: usize = img[0].len();
        let mut result: Vec<Vec<i32>> = vec![vec![0; n]; m];
        for index_m in 0..m {
            for index_n in 0..n {
                let mut summarize: i32 = 0;
                let mut amount: i32 = 0;
                for offset_m in -1..=1 {
                    let index_m_next: i32 = index_m as i32 + offset_m;
                    if index_m_next >= m as i32 || index_m_next < 0 {
                        continue;
                    }

                    for offset_n in -1..=1 {
                        let index_n_next: i32 = index_n as i32 + offset_n;
                        if index_n_next >= n as i32 || index_n_next < 0 {
                            continue;
                        }

                        summarize += img[index_m_next as usize][index_n_next as usize];
                        amount += 1;
                    }
                }

                result[index_m][index_n] = summarize / amount;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(M*N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def imageSmoother(self, img: List[List[int]]) -> List[List[int]]:
        m = len(img)
        n = len(img[0])
        result = [[0]*n for _ in range(m)]
        for index_m in range(m):
            for index_n in range(n):
                summarize = img[index_m][index_n]
                amount = 1
                for offset_m, offset_n in [[-1, -1], [-1, 0], [-1, 1], [0, -1], [0, 1], [1, -1], [1, 0], [1, 1]]:
                    index_m_next = index_m + offset_m
                    index_n_next = index_n + offset_n
                    if index_m_next < 0 or index_m_next >= m or index_n_next < 0 or index_n_next >= n:
                        continue

                    amount += 1
                    summarize += img[index_m_next][index_n_next]

                result[index_m][index_n] = summarize // amount

        return result
```
