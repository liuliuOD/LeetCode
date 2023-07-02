![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1601. [Maximum Number Of Achievable Transfer Requests](https://leetcode.com/problems/maximum-number-of-achievable-transfer-requests)

### Solution :

Method 1 (Backtracking) :
```python
class Solution:
    def maximumRequests(self, n: int, requests: List[List[int]]) -> int:
        self.memoization = defaultdict(int)
        self.requests = requests
        return self.backtracking(0, 0)
    
    def backtracking(self, index_request: int, achievable_request_amount: int) -> int:
        if index_request == len(self.requests):
            for item in self.memoization.values():
                if item == 0:
                    continue
                return 0
            return achievable_request_amount
        
        current_request_start, current_request_target = self.requests[index_request]
        index_next_request = index_request + 1
        
        # use current request
        self.memoization[current_request_start] -= 1
        self.memoization[current_request_target] += 1
        result = self.backtracking(index_next_request, achievable_request_amount+1)

        # drop current request
        self.memoization[current_request_start] += 1
        self.memoization[current_request_target] -= 1
        return max(result, self.backtracking(index_next_request, achievable_request_amount))
```
