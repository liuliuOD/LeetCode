![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 735. [Asteroid Collision](https://leetcode.com/problems/asteroid-collision)

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        result = list(range(len(asteroids)))
        amount_previous = -1
        while amount_previous != len(result):

            amount_previous = len(result)
            temp_result = []
            for index in range(amount_previous):
                current_asteroid = asteroids[result[index]]
                if current_asteroid < 0:
                    index_previous = index - 1
                    previous_asteroid = asteroids[result[index_previous]] if index_previous < amount_previous else None
                    # only append asteroid valid in following rules 1) the first asteroid is negative, 2) previous asteroid is positive and size equal to current asteroid, 3) previous asteroid is negative
                    if index_previous < 0 or (result[index_previous] not in temp_result and previous_asteroid+current_asteroid != 0 and result[index] not in temp_result) or previous_asteroid < 0:
                        temp_result.append(result[index])
                    continue

                index_next = index + 1
                next_asteroid = asteroids[result[index_next]] if index_next < amount_previous else None
                if next_asteroid is None or next_asteroid > 0:
                    temp_result.append(result[index])
                    continue

                # two asteroids' size is the same and move in opposite direction
                if current_asteroid+next_asteroid == 0:
                    continue

                # remain the largest asteroid
                if abs(current_asteroid) > abs(next_asteroid):
                    temp_result.append(result[index])
                elif abs(current_asteroid) < abs(next_asteroid):
                    temp_result.append(result[index_next])

            result = temp_result

        return [asteroids[index] for index in result]
```

Method 2 :
```python
class Solution:
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        n = len(asteroids)
        index_previous = 0
        for index in range(n):
            if asteroids[index] > 0:
                asteroids[index_previous] = asteroids[index]
                index_previous += 1
                continue
            
            while index_previous > 0 and asteroids[index_previous-1] > 0:
                index_temp = index_previous - 1
                if asteroids[index_temp] > -asteroids[index]:
                    asteroids[index] = 0
                    break
                elif asteroids[index_temp] < -asteroids[index]:
                    index_previous = index_temp
                else:
                    index_previous = index_temp
                    asteroids[index] = 0
                    break
            
            if asteroids[index] != 0:
                asteroids[index_previous] = asteroids[index]
                index_previous += 1
        
        return asteroids[:index_previous]
```

Method 3 (Stack) :
```python
class Solution:
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        stack = []
        for asteroid in asteroids:
            stack.append(asteroid)
            while stack and len(stack) >= 2 and stack[-1] < 0 < stack[-2]:
                if abs(stack[-1]) == stack[-2]:
                    stack.pop()
                    stack.pop()
                elif abs(stack[-1]) > stack[-2]:
                    stack.pop()
                    stack.pop()
                    stack.append(asteroid)
                elif abs(stack[-1]) < stack[-2]:
                    stack.pop()

        return stack
```
