![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 3153. [Sum Of Digit Differences Of All Pairs](https://leetcode.com/problems/sum-of-digit-differences-of-all-pairs)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn sum_digit_differences(nums: Vec<i32>) -> i64 {
        let d: usize = nums[0].to_string().len();
        let mut counter: Vec<[i32; 10]> = vec![[0; 10]; d];
        for &num in nums.iter() {
            let mut num: i32 = num;
            let mut index: usize = 0;
            while num > 0 {
                counter[index][(num%10) as usize] += 1;
                num /= 10;
                index += 1;
            }
        }

        let n: i64 = nums.len() as i64;
        let mut result: i64 = 0;
        for index in 0..d {
            for digit in 0..=9 {
                let current: i64 = counter[index][digit] as i64;
                result += current * (n - current);
            }
        }

        return result / 2
    }
}
```

### Solution :

Method 1 (In weekly contest 398, Time Complexity: $O(N*D)$ (N: length of `nums`, D: the number of digits, since it is bounded by a constant (at most 10), we can say it is $O(N)$), Space Complexity: $O(N*D)$ (same with the time complexity, $O(N)$)) :
```python
class Solution:
    def sumDigitDifferences(self, nums: List[int]) -> int:
        # by number of digits
        # calculate frequency of numbers
        counter = defaultdict(lambda: defaultdict(int))
        for num in nums:
            index_digit = 0
            while num > 0:
                counter[index_digit][num%10] += 1
                num //= 10
                index_digit += 1

        result = 0
        n = len(counter)
        for index_digit in range(n):
            counter_current = counter[index_digit]
            for number1, number2 in combinations(counter_current.keys(), 2):
                result += counter_current[number1] * counter_current[number2]

        return result
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def sumDigitDifferences(self, nums: List[int]) -> int:
        counter = defaultdict(lambda: defaultdict(int))
        for num in nums:
            index_digit = 0
            while num > 0:
                counter[index_digit][num%10] += 1
                num //= 10
                index_digit += 1

        n = len(counter)
        # Option 1
        result = 0
        for index_digit in range(n):
            counter_current = counter[index_digit]
            for number in counter_current.keys():
                result += counter_current[number] * (len(nums)-counter_current[number])

        return result // 2
        """
        # Option 2

        return sum(reduce(lambda amount, digit: amount + counter[index_digit][digit]*(len(nums) - counter[index_digit][digit]), counter[index_digit].keys(), 0) for index_digit in range(n)) // 2
        """
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
import "strconv"
func sumDigitDifferences(nums []int) int64 {
    var d int = len(strconv.Itoa(nums[0]))
    var counter = make([][10]int, d)
    for _, num := range nums {
        for i := 0;num > 0; num /= 10 {
            counter[i][num%10] += 1
            i++
        }
    }

    var n int = len(nums)
    var result int64
    for i := 0; i < d; i++ {
        for _, amount := range counter[i] {
            result += int64((n-amount) * amount)
        }
    }

    return result / 2
}
```
