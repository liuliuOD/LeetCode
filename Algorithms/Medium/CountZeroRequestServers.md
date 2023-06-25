![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2747. [Count Zero Request Servers](https://leetcode.com/problems/count-zero-request-servers)

### Solution :

Method 1 (Sliding Window) :
```python
class Solution:
    def countServers(self, n: int, logs: List[List[int]], x: int, queries: List[int]) -> List[int]:
        logs.sort(key=lambda x: x[1])
        
        result = [None for _ in range(len(queries))]
        base = n
        server_trigger_times_in_range = [0 for _ in range(n+1)]
        pointer_left = 0
        pointer_right = 0
        queries = sorted(enumerate(queries), key=lambda x: x[1], reverse=True)
        while queries:
            index_result, time_query = queries.pop()
            while pointer_right < len(logs) and logs[pointer_right][1] <= time_query:
                server_id, time = logs[pointer_right]
                if server_trigger_times_in_range[server_id] == 0:
                    base -= 1
                server_trigger_times_in_range[server_id] += 1
                pointer_right += 1

            while pointer_left < len(logs) and logs[pointer_left][1] < (time_query-x):
                server_id, time = logs[pointer_left]
                print(f'{server_id}, {time}')
                server_trigger_times_in_range[server_id] -= 1
                if server_trigger_times_in_range[server_id] == 0:
                    base += 1
                pointer_left += 1
            result[index_result] = base

        return result
```
