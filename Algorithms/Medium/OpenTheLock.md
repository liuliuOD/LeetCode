![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 752. [Open The Lock](https://leetcode.com/problems/open-the-lock)

### Solution :

Method 1 (BFS, Time Complexity: $O(4*(N+10^4))$ (N: length of `deadends`), Space Complexity: $O(4*(N+10^4))$) :
```python
SLOT_MOVES: List[Dict[str, str]] = [
    # NEXT
    {
        "0": "1",
        "1": "2",
        "2": "3",
        "3": "4",
        "4": "5",
        "5": "6",
        "6": "7",
        "7": "8",
        "8": "9",
        "9": "0",
    },
    # PREVIOUS
    {
        "1": "0",
        "2": "1",
        "3": "2",
        "4": "3",
        "5": "4",
        "6": "5",
        "7": "6",
        "8": "7",
        "9": "8",
        "0": "9",
    }
]
BASE: str = "0000"

class Solution:
    def openLock(self, deadends: List[str], target: str) -> int:
        visited = set(deadends)
        result: int = -1
        if BASE in visited:
            return result

        visited.add(BASE)
        queue = deque([BASE])
        while queue:
            result += 1

            amount = len(queue)
            for _ in range(amount):
                current = queue.popleft()
                print(current)
                if current == target:
                    return result

                for index_slot in range(4):
                    for index_direction in range(2):
                        current_list = list(current)
                        current_list[index_slot] = SLOT_MOVES[index_direction][current_list[index_slot]]

                        next_lock = ''.join(current_list)
                        if next_lock in visited:
                            continue
                        visited.add(next_lock)
                        queue.append(next_lock)

        # can't open the lock
        return -1
```
