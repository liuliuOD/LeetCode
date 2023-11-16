![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1980. [Find Unique Binary String](https://leetcode.com/problems/find-unique-binary-string)

### Solution :

Method 1 (Cantor's Diagonal Argument) :
```rust
impl Solution {
    pub fn find_different_binary_string(mut nums: Vec<String>) -> String {
        return nums.iter().enumerate().map(|(index, string)| match string[index..index+1].to_string().as_str() {
            "0" => "1".to_string(),
            "1" => "0".to_string(),
            _ => "".to_string(),
        }).collect::<String>()
    }
}
```

### Solution :

Method 1 (Trie Tree) :
```python
class Node:
    def __init__(self, bit=None):
        self.children: List[Node] = [None] * 2

class Trie:
    def __init__(self, n: int):
        self.n = n
        self.root = Node()

    def insert(self, string: str):
        node = self.root
        for char in string:
            index = ord(char) - ord("0")
            if node.children[index] is None:
                node.children[index] = Node(char)

            node = node.children[index]

    def findResult(self) -> str:
        queue = deque([(self.root, "")])
        while queue:
            node, result = queue.popleft()
            if node.children[0] is None:
                return result + "0" * (self.n-len(result))
            if node.children[1] is None:
                return result + "1" + "0" * (self.n-len(result)-1)

            queue.append((node.children[0], result + "0"))
            queue.append((node.children[1], result + "1"))

class Solution:
    def findDifferentBinaryString(self, nums: List[str]) -> str:
        trie = Trie(len(nums))
        for string in nums:
            trie.insert(string)

        return trie.findResult()
```

Method 2 (Hash Map) :
```python
class Solution:
    def findDifferentBinaryString(self, nums: List[str]) -> str:
        bitmap = [None, None]
        for binary_string in nums:
            current = bitmap
            for char in binary_string:
                index = ord(char) - ord("0")
                if current[index] is None:
                    current[index] = [None, None]

                current = current[index]

        n = len(nums)
        queue = deque([(bitmap, "")])
        while queue:
            current, result = queue.popleft()
            if current[0] is None:
                return result + "0" * (n-len(result))
            if current[1] is None:
                return result + "1" + "0" * (n-len(result)-1)

            queue.append((current[0], result+"0"))
            queue.append((current[1], result+"1"))
```

Method 3 (Hash Set) :
```python
class Solution:
    def findDifferentBinaryString(self, nums: List[str]) -> str:
        existed = set()
        for num in nums:
            existed.add(int(num, 2))

        n = len(nums)
        for num in range(n+1):
            if num in existed:
                continue

            num_binary = bin(num)[2:]
            return "0" * (n-len(num_binary)) + num_binary
```

Method 4 (Random Sampling, this method is suitable when `n` becomes larger and larger) :
```python
class Solution:
    def findDifferentBinaryString(self, nums: List[str]) -> str:
        existed = set()
        for num in nums:
            existed.add(int(num, 2))

        n = len(nums)
        result = int(nums[0], 2)
        while result in existed:
            result = random.randrange(0, 2**n)

        num_binary = bin(result)[2:]
        return "0" * (n-len(num_binary)) + num_binary
```

Method 5 (Cantor's Diagonal Argument, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (the space that result used isn't included in when calculating complexity)) :
```python
class Solution:
    def findDifferentBinaryString(self, nums: List[str]) -> str:
        return ''.join(["0" if nums[index][index] == "1" else "1" for index in range(len(nums))])
```
