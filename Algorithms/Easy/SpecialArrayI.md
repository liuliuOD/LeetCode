![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 3151. [Special Array I](https://leetcode.com/problems/special-array-i)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`) :
```rust
impl Solution {
    pub fn is_array_special(nums: Vec<i32>) -> bool {
        for index in 1..nums.len() {
            if nums[index-1]%2 == nums[index]%2 {
                return false
            }
        }

        return true
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`) :
```python
class Solution:
    def isArraySpecial(self, nums: List[int]) -> bool:
        n = len(nums)
        for index in range(1, n):
            if nums[index] % 2 == nums[index-1] % 2:
                return False

        return True
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`) :
```python
class Solution {
    public boolean isArraySpecial(int[] nums) {
        for (int index=1; index<nums.length; index++) {
            if (nums[index-1]%2 == nums[index]%2) {
                return false;
            }
        }

        return true;
    }
}
```
