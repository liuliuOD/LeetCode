![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2951. [Find The Peaks](https://leetcode.com/problems/find-the-peaks)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn find_peaks(mountain: Vec<i32>) -> Vec<i32> {
        let mut result: Vec<i32> = vec![];
        for index in 1..mountain.len()-1 {
            if mountain[index] <= mountain[index-1] || mountain[index] <= mountain[index+1] {
                continue;
            }

            result.push(index as i32);
        }

        return result
    }
}
```

### Solution :

Method 1 (In weekly contest 374) :
```python
class Solution:
    def findPeaks(self, mountain: List[int]) -> List[int]:
        result = []
        for index in range(1, len(mountain)-1):
            if mountain[index-1] < mountain[index] and mountain[index] > mountain[index+1]:
                result.append(index)

        return result
```
