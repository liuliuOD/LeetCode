![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 179. [Largest Number](https://leetcode.com/problems/largest-number)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the element in `nums`)) :
```rust
impl Solution {
    pub fn largest_number(mut nums: Vec<i32>) -> String {
        nums.sort_unstable_by_key(|value| value.to_string().repeat(10));
        nums.reverse();

        if nums[0] == 0 {
            return "0".to_string()
        }

        return nums
            .iter()
            .fold(String::new(), |a, b| a + &b.to_string())
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the element in `nums`)) :
```python
class Solution:
    def largestNumber(self, nums: List[int]) -> str:
        nums.sort(key=lambda value: str(value) * 10, reverse=True)

        if nums[0] == 0:
            return "0"

        return "".join(str(num) for num in nums)
```
