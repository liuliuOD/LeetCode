![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 1208. [Get Equal Substrings Within Budget](https://leetcode.com/problems/get-equal-substrings-within-budget)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn equal_substring(s: String, t: String, max_cost: i32) -> i32 {
        let n: usize = s.len();
        let s_ascii: Vec<i32> = s.bytes().map(|ascii| ascii as i32).collect::<Vec<i32>>();
        let t_ascii: Vec<i32> = t.bytes().map(|ascii| ascii as i32).collect::<Vec<i32>>();
        let mut index_start: usize = 0;
        let mut cost_sum: i32 = 0;
        let mut result: i32 = 0;
        for index_end in 0..n {
            cost_sum += (s_ascii[index_end] - t_ascii[index_end]).abs();
            while cost_sum > max_cost {
                cost_sum -= (s_ascii[index_start] - t_ascii[index_start]).abs();
                index_start += 1;
            }

            result = result.max((index_end - index_start + 1) as i32);
        }

        return result
    }
}
```

Method 2 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn equal_substring(s: String, t: String, mut max_cost: i32) -> i32 {
        let n: usize = s.len();
        let s_ascii: Vec<u8> = s.into_bytes();
        let t_ascii: Vec<u8> = t.into_bytes();
        let mut index_start: usize = 0;
        let mut result: i32 = 0;
        for index_end in 0..n {
            max_cost -= u8::abs_diff(s_ascii[index_end], t_ascii[index_end]) as i32;
            while max_cost < 0 {
                max_cost += u8::abs_diff(s_ascii[index_start], t_ascii[index_start]) as i32;
                index_start += 1;
            }

            /* Option 1 */
            result = result.max((index_end - index_start + 1) as i32);
            /* Option 2

            result = i32::max(result, (index_end - index_start + 1) as i32);
            */
        }

        return result
    }
}
```

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def equalSubstring(self, s: str, t: str, max_cost: int) -> int:
        costs = [abs(ord(char_s)-ord(char_t)) for char_s, char_t in zip(s, t)]
        result = 0
        cost_sum = 0
        index_start = 0
        for index_end in range(len(s)):
            cost_sum += costs[index_end]
            if cost_sum <= max_cost:
                result = max(result, index_end - index_start + 1)
            else:
                while cost_sum > max_cost:
                    cost_sum -= costs[index_start]
                    index_start += 1

        return result
```

Method 2 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def equalSubstring(self, s: str, t: str, max_cost: int) -> int:
        result = 0
        cost_sum = 0
        index_start = 0
        for index_end in range(len(s)):
            cost_sum += abs(ord(s[index_end])-ord(t[index_end]))
            if cost_sum <= max_cost:
                result = max(result, index_end - index_start + 1)
            else:
                while cost_sum > max_cost:
                    cost_sum -= abs(ord(s[index_start])-ord(t[index_start]))
                    index_start += 1

        return result
```

Method 3 (Two Pointer + Refactoring, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def equalSubstring(self, s: str, t: str, max_cost: int) -> int:
        result = 0
        cost_sum = 0
        index_start = 0
        for index_end in range(len(s)):
            cost_sum += self.get_cost(index_end, s, t)
            if cost_sum <= max_cost:
                result = max(result, index_end - index_start + 1)
            else:
                while cost_sum > max_cost:
                    cost_sum -= self.get_cost(index_start, s, t)
                    index_start += 1

        return result

    def get_cost(self, index: int, s: str, t: str) -> int:
        return abs(ord(s[index])-ord(t[index]))
```

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```go
func equalSubstring(s string, t string, costMax int) int {
    var result int
    var costSum int
    var indexStart int
    for indexEnd := 0; indexEnd < len(s); indexEnd++ {
        cost := int(s[indexEnd]) - int(t[indexEnd])
        if cost < 0 {
            cost *= -1
        }
        costSum += cost
        if costSum <= costMax {
            result = max(result, indexEnd - indexStart + 1)
        } else {
            for costSum > costMax {
                cost := int(s[indexStart]) - int(t[indexStart])
                if cost < 0 {
                    cost *= -1
                }
                costSum -= cost
                indexStart++
            }
        }
    }

    return result
}
```

Method 2 (Two Pointer + Refactoring, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```go
func equalSubstring(s string, t string, costMax int) int {
    var result int
    var costSum int
    var indexStart int
    for indexEnd := 0; indexEnd < len(s); indexEnd++ {
        costSum += abs(int(s[indexEnd]) - int(t[indexEnd]))
        if costSum <= costMax {
            result = max(result, indexEnd - indexStart + 1)
        } else {
            for costSum > costMax {
                costSum -= abs(int(s[indexStart]) - int(t[indexStart]))
                indexStart++
            }
        }
    }

    return result
}

func abs(num int) int {
    if num < 0 {
        return -num
    }

    return num
}
```
