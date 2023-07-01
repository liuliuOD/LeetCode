![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2305. [Fair Distribution Of Cookies](https://leetcode.com/problems/total-cost-to-hire-k-workers)

### Solution :

Method 1 (Backtracking, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def distributeCookies(self, cookies: List[int], k: int) -> int:
        self.k = k
        self.cookies = cookies
        return self.dfs(0, [0]*k)
    
    def dfs(self, index_cookie: int, distribution_cookies: List[list]) -> int:
        if index_cookie >= len(self.cookies):
            return max(distribution_cookies)
        
        result = float('inf')
        for index_k in range(self.k):
            temp = distribution_cookies.copy()
            temp[index_k] += self.cookies[index_cookie]
            result = min(result, self.dfs(index_cookie+1, temp))
        return result
```

Method 2 (Backtracking + Pruning, use copy to record cookies distribution, Time Complexity: $O(K^N)$ -> K: children amount, N: cookies amount) :
```python
class Solution:
    def distributeCookies(self, cookies: List[int], k: int) -> int:
        self.k = k
        self.cookies = cookies
        return self.dfs(0, [0]*k)
    
    def dfs(self, index_cookie: int, distribution_cookies: List[list]) -> int:
        if index_cookie >= len(self.cookies):
            return max(distribution_cookies)
        
        result = float('inf')
        for index_k in range(self.k):
            temp = distribution_cookies.copy()
            temp[index_k] += self.cookies[index_cookie]
            if max(temp) >= result:
                continue
            result = min(result, self.dfs(index_cookie+1, temp))
        return result
```

Method 3 (Backtracking + Pruning, use a shard variable to record cookies distribution, Time Complexity: $O(K^N)$ -> K: children amount, N: cookies amount) :
```python
class Solution:
    def distributeCookies(self, cookies: List[int], k: int) -> int:
        self.k = k
        self.cookies = cookies
        self.memoization = [0]*k
        return self.dfs(0)
    
    def dfs(self, index_cookie: int) -> int:
        if index_cookie >= len(self.cookies):
            return max(self.memoization)
        
        result = float('inf')
        for index_k in range(self.k):
            self.memoization[index_k] += self.cookies[index_cookie]
            if result > max(self.memoization):
                result = min(result, self.dfs(index_cookie+1))

            self.memoization[index_k] -= self.cookies[index_cookie]
        return result
```

Method 4 (Binary Search + Bitmask) :
```python
class Solution:
    def distributeCookies(self, cookies: List[int], k: int) -> int:
        pointer_left = min(cookies)
        pointer_right = sum(cookies)

        while pointer_left < pointer_right:
            self.cookie_unfairness = pointer_left + (pointer_right - pointer_left) // 2

            if self.canDistribute(cookies, k):
                pointer_right = self.cookie_unfairness
            else:
                pointer_left = self.cookie_unfairness + 1
        return pointer_left
    
    def canDistribute(self, available_cookies: List[int], k: int) -> bool:
        if k == 1:
            return sum(available_cookies) <= self.cookie_unfairness

        current_cookie_amount = len(available_cookies)
        for mask_cookie in range(1, 1<<current_cookie_amount):
            choosed_cookie_amount = 0
            available = []
            for index_cookie in range(current_cookie_amount):
                if mask_cookie & 1<<index_cookie:
                    choosed_cookie_amount += available_cookies[index_cookie]
                else:
                    available.append(available_cookies[index_cookie])
            
            if choosed_cookie_amount > self.cookie_unfairness:
                continue
            
            if self.canDistribute(available, k-1):
                return True
        return False
```
