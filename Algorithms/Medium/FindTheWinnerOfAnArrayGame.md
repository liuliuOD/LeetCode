![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1535. [Find The Winner Of An Array Game](https://leetcode.com/problems/find-the-winner-of-an-array-game)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn get_winner(arr: Vec<i32>, k: i32) -> i32 {
        let mut result: i32 = arr[0];
        let mut win: i32 = 0;
        /* Option 1 */
        for index in 1..arr.len() {
            if result > arr[index] {
                win += 1;
            } else {
                win = 1;
                result = arr[index];
            }

            if win == k {
                break;
            }
        }
        /* Option 2

        for &item in arr.iter().skip(1) {
            if result > item {
                win += 1;
            } else {
                win = 1;
                result = item;
            }

            if win == k {
                break;
            }
        }
        */
        /* Option 3

        arr.iter().skip(1).for_each(|&item| {
            if win == k {
                return
            }

            if result > item {
                win += 1;
            } else {
                win = 1;
                result = item;
            }
        });
        */

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def getWinner(self, arr: List[int], k: int) -> int:
        n = len(arr)
        maximum = max(arr)
        if k >= n:
            return maximum

        arr = deque(arr)
        current = arr[0]
        win = 0
        while win < k:
            if current == maximum:
                break

            if arr[0] > arr[1]:
                win += 1
                arr.popleft()
                arr.rotate(-1)
                arr.appendleft(current)
            elif arr[0] < arr[1]:
                current = arr[1]
                win = 1
                arr.rotate(-1)

        return current
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def getWinner(self, arr: List[int], k: int) -> int:
        n = len(arr)
        maximum = max(arr)
        if k >= n:
            return maximum

        arr = deque(arr)
        win = 0
        # Option 1
        while win < k:
            current = arr.popleft()
            if current == maximum:
                break

            second = arr.popleft()
            if current > second:
                win += 1
                arr.append(second)
                arr.appendleft(current)
            else:
                win = 1
                current = second
                arr.appendleft(second)
                arr.append(current)
        """
        # Option 2

        current = arr.popleft()
        while win < k:
            if current == maximum:
                break

            second = arr.popleft()
            if current > second:
                win += 1
                arr.append(second)
            else:
                win = 1
                current = second
                arr.append(current)
        """

        return current
```

Method 3 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def getWinner(self, arr: List[int], k: int) -> int:
        maximum = max(arr)
        win = 0
        current = arr[0]

        """
        using `for index in range(1, len(arr))` is faster and conserves more memory than using `for item in arr[1:]:`
        """
        for index in range(1, len(arr)):
            if current > arr[index]:
                win += 1
            else:
                win = 1
                current = arr[index]

            if win == k or current == maximum:
                break

        return current
```
