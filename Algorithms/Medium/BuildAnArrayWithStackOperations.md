![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1441. [Build An Array With Stack Operations](https://leetcode.com/problems/build-an-array-with-stack-operations)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn build_array(target: Vec<i32>, n: i32) -> Vec<String> {
        let mut result: Vec<String> = vec![];
        let mut current: i32 = 1;
        for item in target {
            while current < item {
                /* Option 1 */
                result.push("Push".to_string());
                result.push("Pop".to_string());
                /* Option 2

                result.append(&mut vec!["Push".to_string(), "Pop".to_string()]);
                */
                current += 1;
            }

            result.push("Push".to_string());
            current += 1;
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def buildArray(self, target: List[int], n: int) -> List[str]:
        result = []
        left = 1
        for item in target:
            while left < item:
                left += 1
                result += ['Push', 'Pop']

            result.append('Push')
            left += 1

        return result
```

Method 2 (Better Coding Style, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
from enum import Enum
class Operation(Enum):
    PUSH = 'Push'
    POP = 'Pop'

class Solution:
    def buildArray(self, target: List[int], n: int) -> List[str]:
        result = []
        left = 1
        for item in target:
            while left < item:
                left += 1
                result += [Operation.PUSH.value, Operation.POP.value]

            result.append(Operation.PUSH.value)
            left += 1

        return result
```

Method 3 (Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def buildArray(self, target: List[int], n: int) -> List[str]:
        stack = []
        result = []
        pointer = 0
        for current in range(1, n+1):
            stack.append(current)
            result.append('Push')
            if stack[-1] == target[pointer]:
                pointer += 1
            else:
                stack.pop()
                result.append('Pop')

            if pointer >= len(target):
                return result
```
