![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2751. [Robot Collisions](https://leetcode.com/problems/robot-collisions)

### Solution :

Method 1 (Binary Heap + Binary Search) :
```python
class Solution:
    def survivedRobotsHealths(self, positions: List[int], healths: List[int], directions: str) -> List[int]:
        n = len(positions)
        move_left, move_right = [], []
        for index in range(n):
            status = [positions[index], healths[index], index]
            if directions[index] == 'L':
                heapq.heappush(move_left, status)
            else:
                move_right.append(status)

        move_right.sort()
        result = []
        while move_right and move_left:
            position, health, index = heapq.heappop(move_left)
            index_move_right = self.find_move_right_index(position_left=position, move_right=move_right)
            if index_move_right is not None:
                offset = 0
                while index_move_right-offset >= 0:
                    health_right = move_right[index_move_right-offset][1]
                    if health_right >= health:
                        if health_right > health:
                            move_right[index_move_right-offset][1] -= 1
                            offset -= 1

                        health = 0
                        break

                    health -= 1
                    offset += 1

                move_right[max(0, index_move_right-offset):index_move_right+1] = []

            if health > 0:
                result.append((index, health))

        if move_right:
            result.extend((index, health) for _, health, index in move_right)
        elif move_left:
            result.extend((index, health) for _, health, index in move_left)

        return [item[1] for item in sorted(result, key=lambda item: item[0])]

    def find_move_right_index(self, position_left: int, move_right: list[list[int]]) -> int | None:
        left, right = 0, len(move_right) - 1
        while left <= right:
            middle = left + (right - left)//2
            if move_right[middle][0] < position_left:
                left = middle + 1
            else:
                right = middle - 1

        return None if right < 0 else right
```

Method 2 (Binary Heap + Binary Search) :
```python
class Solution:
    def survivedRobotsHealths(self, positions: List[int], healths: List[int], directions: str) -> List[int]:
        n = len(positions)
        move_left, move_right = [], []
        for index in range(n):
            status = [positions[index], healths[index], index]
            if directions[index] == 'L':
                heapq.heappush(move_left, status)
            else:
                move_right.append(status)

        move_right.sort(reverse=True)
        result = []
        while move_right and move_left:
            position, health, index = heapq.heappop(move_left)
            index_move_right = self.find_move_right_index(position_left=position, move_right=move_right)
            if index_move_right is not None:
                while index_move_right < len(move_right):
                    health_right = move_right[index_move_right][1]
                    if health_right >= health:
                        if health_right > health:
                            move_right[index_move_right][1] -= 1
                        else:
                            move_right.pop(index_move_right)

                        health = 0
                        break

                    health -= 1
                    move_right.pop(index_move_right)

            if health > 0:
                result.append((index, health))

        if move_right:
            result.extend((index, health) for _, health, index in move_right)
        elif move_left:
            result.extend((index, health) for _, health, index in move_left)

        return [item[1] for item in sorted(result, key=lambda item: item[0])]

    def find_move_right_index(self, position_left: int, move_right: list[list[int]]) -> int | None:
        n = len(move_right)
        left, right = 0, n - 1
        while left <= right:
            middle = left + (right - left)//2
            if move_right[middle][0] < position_left:
                right = middle - 1
            else:
                left = middle + 1

        return None if left >= n else left
```

Method 3 (Sorted + Stack, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: number of the elements in `positions`)) :
```python
class Solution:
    def survivedRobotsHealths(self, positions: List[int], healths: List[int], directions: str) -> List[int]:
        n = len(positions)
        positions_sorted = sorted(enumerate(positions), key=lambda item: item[1])

        stack_right = []
        for index in range(n):
            index_current = positions_sorted[index][0]
            if directions[index_current] == 'R':
                stack_right.append(index_current)
            elif directions[index_current] == 'L':
                while stack_right:
                    index_right = stack_right[-1]
                    health_right = healths[index_right]
                    health_left = healths[index_current]
                    if health_right > health_left:
                        healths[index_right] -= 1
                        healths[index_current] = 0
                        break
                    elif health_right == health_left:
                        healths[index_right] = 0
                        stack_right.pop()
                        healths[index_current] = 0
                        break
                    else:
                        healths[index_right] = 0
                        stack_right.pop()
                        healths[index_current] -= 1

        return list(filter(lambda health: health > 0, healths))
```
