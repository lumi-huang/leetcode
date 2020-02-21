
### 1091. Shortest Path in Binary Matrix
```python
class Solution:
    def shortestPathBinaryMatrix(self, grid: List[List[int]]) -> int:
        if grid[0][0] or grid[-1][-1]:
            return -1
        n = len(grid)
        queue = collections.deque([(0,0,1)])
        while queue:
            i,j,d = queue.popleft()
            if i == n-1 and j == n-1:
                return d
            for x, y in [(i-1,j-1),(i-1,j),(i-1,j+1),(i,j-1),(i,j+1),(i+1,j-1),(i+1,j),(i+1,j+1)]:
                if 0 <= x < n and 0 <= y < n and not grid[x][y]:
                    grid[x][y] = 1
                    queue.append((x, y, d+1))
        return -1
```

### 279. Perfect Squares
```python
class Solution:
    def numSquares(self, n: int) -> int:
        queue = collections.deque([(0, 0)])
        visited = set()
        while queue:
            i, step = queue.popleft()
            for j in range(n+1):
                sum_square = i+j*j
                if sum_square == n:
                    return step+1
                if sum_square > n:
                    break
                if sum_square not in visited:
                    visited.add(sum_square)
                    queue.append((sum_square, step+1))
```
