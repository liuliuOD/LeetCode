![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 3005. [Count Elements With Maximum Frequency](https://leetcode.com/problems/count-elements-with-maximum-frequency)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn max_frequency_elements(nums: Vec<i32>) -> i32 {
        let mut counter: [i32; 100] = [0; 100];
        for num in nums {
            counter[(num-1) as usize] += 1;
        }

        let maximum: i32 = *counter.iter().max().unwrap();
        return counter.into_iter().filter(|&x| x == maximum).sum()
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maxFrequencyElements(self, nums: List[int]) -> int:
        counter = Counter(nums)
        maximum = max(counter.values())

        return sum([num for num in counter.values() if num == maximum])
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func maxFrequencyElements(nums []int) int {
    counter := [100]int{}
    for _, num := range nums {
        counter[num-1]++
    }

    maximum := 0
    result := 0
    for index := 0; index < 100; index++ {
        if counter[index] < maximum {
            continue
        } else if counter[index] > maximum {
            maximum = counter[index]
            result = maximum
        } else {
            result += maximum
        }
    }

    return result
}
```
