![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2037. [Minimum Number Of Moves To Seat Everyone](https://leetcode.com/problems/minimum-number-of-moves-to-seat-everyone)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn min_moves_to_seat(mut seats: Vec<i32>, mut students: Vec<i32>) -> i32 {
        seats.sort();
        students.sort();
        let mut result: i32 = 0;
        for index in 0..seats.len() {
            result += (seats[index] - students[index]).abs();
        }

        return result
    }
}
```

Method 2 (Radix Sort, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn min_moves_to_seat(seats: Vec<i32>, students: Vec<i32>) -> i32 {
        let seats = Self::radix_sort(&seats);
        let students = Self::radix_sort(&students);
        let mut result: i32 = 0;
        for index in 0..seats.len() {
            result += (seats[index] - students[index]).abs();
        }

        return result
    }

    fn radix_sort(nums: &Vec<i32>) -> Vec<i32> {
        let mut result: Vec<i32> = nums.clone();
        for bit in 0..7 {
            Self::bucket_sort(&mut result, bit);
        }

        return result
    }

    fn bucket_sort(mut nums: &mut Vec<i32>, bit: usize) {
        let mut buckets: Vec<Vec<i32>> = vec![vec![]; 2];
        for num in nums.iter() {
            buckets[((*num >> bit)&1) as usize].push(*num);
        }

        let mut index: usize = 0;
        for group in buckets {
            for num in group {
                nums[index] = num;
                index += 1;
            }
        }
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minMovesToSeat(self, seats: List[int], students: List[int]) -> int:
        seats.sort()
        students.sort()
        result = 0
        n = len(seats)
        for index in range(n):
            result += abs(seats[index]-students[index])

        return result
```

Method 2 (Counting Sort, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minMovesToSeat(self, seats: List[int], students: List[int]) -> int:
        seats = self.counting_sort(seats)
        students = self.counting_sort(students)
        result = 0
        n = len(seats)
        for index in range(n):
            result += abs(seats[index]-students[index])

        return result

    def counting_sort(self, nums: list[int]) -> list[int]:
        counter = [0] * 101
        for num in nums:
            counter[num] += 1

        result = [0] * len(nums)
        index = 0
        for num in range(1, 101):
            amount = counter[num]
            result[index:index+amount] = [num] * amount
            index += amount

        return result
```

Method 3 (Radix Sort, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minMovesToSeat(self, seats: List[int], students: List[int]) -> int:
        seats = self.radix_sort(seats)
        students = self.radix_sort(students)
        result = 0
        n = len(seats)
        for index in range(n):
            result += abs(seats[index]-students[index])

        return result

    def radix_sort(self, nums: list[int]) -> list[int]:
        for bit in range(7):
            nums = self.bucket_sort(nums, bit)

        return nums

    def bucket_sort(self, nums: list[int], bit: int) -> list[int]:
        buckets = [[] for _ in range(2)]
        for num in nums:
            buckets[(num >> bit) & 1].append(num)

        result = []
        for group in buckets:
            result.extend(group)

        return result
```
