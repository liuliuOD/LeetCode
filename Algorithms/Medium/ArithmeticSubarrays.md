![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1630. [Arithmetic Subarrays](https://leetcode.com/problems/arithmetic-subarrays)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn check_arithmetic_subarrays(nums: Vec<i32>, l: Vec<i32>, r: Vec<i32>) -> Vec<bool> {
        let mut result: Vec<bool> = vec![];
        for index in 0..l.len() {
            let mut nums_subsequence: Vec<i32> = Vec::from(&nums[l[index] as usize..=r[index] as usize]);
            nums_subsequence.sort();
            let difference: i32 = nums_subsequence[1] - nums_subsequence[0];
            let mut is_arithmetic: bool = true;
            for index_subsequence in 1..(nums_subsequence.len()-1) {
                if nums_subsequence[index_subsequence+1]-nums_subsequence[index_subsequence] == difference {
                    continue;
                }

                is_arithmetic = false;
                break;
            }

            result.push(is_arithmetic);
        }

        return result
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn check_arithmetic_subarrays(nums: Vec<i32>, l: Vec<i32>, r: Vec<i32>) -> Vec<bool> {
        return l.iter().zip(r.iter()).map(|(&left, &right)| Self::is_arithmetic(&nums, left, right)).collect()
    }

    fn is_arithmetic(nums: &Vec<i32>, left: i32, right: i32) -> bool {
        let mut nums_subsequence: Vec<i32> = Vec::from(&nums[left as usize..=right as usize]);
        nums_subsequence.sort();
        return nums_subsequence.windows(2).all(|items| items[1] - items[0] == nums_subsequence[1] - nums_subsequence[0])
    }
}
```

### Solution :

Method 1 (Sort) :
```python
class Solution:
    def checkArithmeticSubarrays(self, nums: List[int], l: List[int], r: List[int]) -> List[bool]:
        result = []
        for index in range(len(l)):
            nums_sorted = sorted(nums[l[index]:r[index]+1])
            difference = nums_sorted[1] - nums_sorted[0]
            # Option 1
            is_arithmetic = True
            for index_sorted in range(1, len(nums_sorted)-1):
                if nums_sorted[index_sorted+1] - nums_sorted[index_sorted] != difference:
                    is_arithmetic = False
                    break

            result.append(is_arithmetic)
            """
            # Option 2

            result.append(all([nums_sorted[index_sorted+1] - nums_sorted[index_sorted] == difference for index_sorted in range(1, len(nums_sorted)-1)]))
            """

        return result
```

Method 2 (Non-Sort) :
```python
class Solution:
    def checkArithmeticSubarrays(self, nums: List[int], l: List[int], r: List[int]) -> List[bool]:
        result = []
        for index in range(len(l)):
            is_arithmetic = True
            nums_subsequence = nums[l[index]:r[index]+1]
            maximum = max(nums_subsequence)
            minimum = min(nums_subsequence)
            nums_set = set(nums_subsequence)
            if (maximum-minimum) % (len(nums_subsequence)-1) != 0:
                is_arithmetic = False
            else:
                difference = (maximum-minimum) // (len(nums_subsequence)-1)
                current = minimum + difference
                while current < maximum:
                    if current not in nums_set:
                        is_arithmetic = False
                        break

                    current += difference

            result.append(is_arithmetic)

        return result
```
