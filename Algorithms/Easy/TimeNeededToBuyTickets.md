![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 2073. [Time Needed To Buy Tickets](https://leetcode.com/problems/time-needed-to-buy-tickets)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M*N)$ (M: value of `tickets[k]`, N: length of `tickets`), Space Complexity: $O(1)$) :
```python
class Solution:
    def timeRequiredToBuy(self, tickets: List[int], k: int) -> int:
        result = 0
        while tickets[k] > 0:
            for index in range(len(tickets)):
                if tickets[index] == 0:
                    continue

                tickets[index] -= 1
                result += 1

                if tickets[index] == 0 and index == k:
                    break

        return result
```

Method 2 (Mathematic, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def timeRequiredToBuy(self, tickets: List[int], k: int) -> int:
        result = 0
        for index in range(len(tickets)):
            if index <= k:
                result += min(tickets[index], tickets[k])
            else:
                result += min(tickets[index], tickets[k]-1)

        return result
```

### Solution :

Method 1 (Mathematic, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```go
func timeRequiredToBuy(tickets []int, k int) int {
    var result int
    for index := 0; index < len(tickets); index++ {
        // Option 1
        if index <= k {
            result += min(tickets[index], tickets[k])
        } else {
            result += min(tickets[index], tickets[k] - 1)
        }
        /*
        // Option 2

        if tickets[index] < tickets[k] {
            result += tickets[index]
        } else if index <= k {
            result += tickets[k]
        } else {
            result += tickets[k] - 1
        }
        */
    }

    return result
}
```
