![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 228. [Summary Ranges](https://leetcode.com/problems/summary-ranges)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn summary_ranges(nums: Vec<i32>) -> Vec<String> {
        let mut result: Vec<String> = vec![];
        let mut left: usize = 0;
        let mut right: usize = 0;

        while left < nums.len() {
            while right+1 < nums.len() && nums[right]+1 == nums[right+1] {
                right += 1;
            }

            match left == right {
                true => result.push(format!("{}", nums[left])),
                false => result.push(format!("{}->{}", nums[left], nums[right])),
            }

            right += 1;
            left = right;
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$) :
```python
class Solution:
    def summaryRanges(self, nums: List[int]) -> List[str]:
        result = list()

        if len(nums) == 0:
            return result

        start = nums[0]
        for index in range(1, len(nums)):
            if nums[index-1]+1 == nums[index]:
                continue
            
            if nums[index-1] == start:
                result.append(f'{start}')
            else:
                result.append(f'{start}->{nums[index-1]}')
            
            start = nums[index]
        
        if nums[-1] == start:
            result.append(f'{start}')
        else:
            result.append(f'{start}->{nums[-1]}')
        
        return result
```

Method 2 :
```python
class Solution:
    def summaryRanges(self, nums: List[int]) -> List[str]:
        result = list()

        if len(nums) == 0:
            return result

        start = nums[0]
        for index in range(len(nums)):
            if index == len(nums)-1:
                result.append(self.assembleResultInfo(nums[index], start))
                break

            if nums[index+1] == nums[index]+1:
                continue
            result.append(self.assembleResultInfo(nums[index], start))
            start = nums[index+1]
        return result
    
    def assembleResultInfo(self, current, start) -> str:
        return f'{start}' if current == start else f'{start}->{current}'
```
