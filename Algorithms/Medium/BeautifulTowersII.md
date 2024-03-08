![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2866. [Beautiful Towers II](https://leetcode.com/problems/beautiful-towers-ii)

### Solution :

Method 1 (Monotonic Stack, ERROR: "Time Limit Exceeded", 777/785, Time Complexity: $O(N^2)$) :
```python
class Solution:
    def maximumSumOfHeights(self, maxHeights: List[int]) -> int:
        n = len(maxHeights)
        if n == 1:
            return maxHeights[0]

        right = [0] * n
        stack = []
        for index in reversed(range(1, n)):
            current = maxHeights[index]
            while stack and stack[-1][0] >= current:
                stack.pop()

            stack.append((current, index))

            sum_current = 0
            len_stack = len(stack)
            for index_stack in range(len_stack):
                height, index_height = stack[index_stack]
                sum_current += (n - index_height) * height if index_stack == 0 else (stack[index_stack-1][1] - index_height) * height

            right[index-1] = sum_current

        left = [0] * n
        stack = []
        for index in range(0, n-1):
            current = maxHeights[index]
            while stack and stack[-1][0] >= current:
                stack.pop()

            stack.append((current, index))

            sum_current = 0
            len_stack = len(stack)
            for index_stack in range(len_stack):
                height, index_height = stack[index_stack]
                sum_current += (index_height+1) * height if index_stack == 0 else (stack[index_stack][1]-stack[index_stack-1][1]) * height

            left[index+1] = sum_current

        result = 0
        for index, current in enumerate(maxHeights):
            if (index == 0 and maxHeights[index] < maxHeights[index+1]) or (index == n-1 and maxHeights[index] < maxHeights[index-1]):
                continue

            if 0 < index < n-1 and (maxHeights[index] < maxHeights[index-1] or maxHeights[index] < maxHeights[index+1]):
                continue

            result = max(result, current + left[index] + right[index])

        return result
```

Method 2 (Monotonic Stack, Time Complexity: $O(N)$) :
```python
class Solution:
    def maximumSumOfHeights(self, max_heights: List[int]) -> int:
        n = len(max_heights)
        if n == 1:
            return max_heights[0]

        right = [0] * n
        sum_current = 0
        stack = []
        for index in reversed(range(n)):
            current = max_heights[index]
            while stack and max_heights[stack[-1]] >= current:
                index_drop = stack.pop()
                amount = stack[-1] - index_drop if stack else n - index_drop
                sum_current -= max_heights[index_drop] * amount

            amount = stack[-1] - index if stack else n - index
            sum_current += current * amount
            right[index] = sum_current

            stack.append(index)

        stack = []
        result = 0
        sum_current = 0
        for index in range(n):
            current = max_heights[index]
            while stack and max_heights[stack[-1]] >= current:
                index_drop = stack.pop()
                amount = index_drop - stack[-1] if stack else index_drop + 1
                sum_current -= max_heights[index_drop] * amount

            amount = index - stack[-1] if stack else index + 1
            sum_current += current * amount

            stack.append(index)

            result = max(result, sum_current + right[index] - current)

        return result
```
