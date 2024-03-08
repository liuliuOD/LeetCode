![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2092. [Find All People With Secret](https://leetcode.com/problems/find-all-people-with-secret)

### Solution :

Method 1 (BFS, Time Complexity: $O((N+M)*M)$ (N: value of `n`, M: length of `meetings`), Space Complexity: $O(N+M)$) :
```python
class Solution:
    def findAllPeople(self, n: int, meetings: List[List[int]], first_person: int) -> List[int]:
        mapping = [[] for _ in range(n)]
        for x, y, t in meetings:
            mapping[x].append((y, t))
            mapping[y].append((x, t))

        times = [inf] * n
        times[0] = times[first_person] = 0
        queue = deque([(0, 0), (first_person, 0)])
        while queue:
            index, time_current = queue.popleft()
            for index_next, time_next in mapping[index]:
                if time_next < time_current or times[index_next] <= time_next:
                    continue

                queue.append((index_next, time_next))
                times[index_next] = time_next

        return [index for index, time in enumerate(times) if time is not inf]
```
