
## **Breadth-First Search (BFS)**  
  
  
### 199. Binary Tree Right Side View
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def rightSideView(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        res = []
        if not root:
            return []
        
        queue = collections.deque([root])
        while queue:
            res.append(queue[-1].val)
            num_node = len(queue)
            for _ in range(num_node):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        
        return res
```

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
Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

Example 1:

Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
Example 2:

Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.

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

### 127. Word Ladder
Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

Only one letter can be changed at a time.
Each transformed word must exist in the word list.
Note:

Return 0 if there is no such transformation sequence.
All words have the same length.
All words contain only lowercase alphabetic characters.
You may assume no duplicates in the word list.
You may assume beginWord and endWord are non-empty and are not the same.
```python
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        if endWord not in wordList:
            return 0
        wordList = set(wordList)
        queue = collections.deque([(beginWord, 1)])
        while queue:
            word, step = queue.popleft()
            if word == endWord:
                return step
            for i in range(len(word)):
                for char in 'abcdefghijklmnopqrstuvwxyz':
                    trans_word = word[0:i]+char+word[i+1:]
                    if trans_word in wordList:
                        queue.append((trans_word, step+1))
                        wordList.remove(trans_word)
        return 0
```

### 102. Binary Tree Level Order Traversal. 
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        traversal = [] #return value
        if not root:
            return traversal
        queue = collections.deque([root])
        
        while queue:
            num_nodes = len(queue)
            temp = [] #temp storage for each binary tree level
            
            for _ in range(num_nodes):
                node = queue.popleft()
                temp.append(node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            traversal.append(temp)
        
        return traversal
```

### 909. Snakes and Ladders
```python
class Solution(object):
    def snakesAndLadders(self, board):
        """
        :type board: List[List[int]]
        :rtype: int
        """
        
        n = len(board)
        visited = set()
        
        #given a square sum s, return board coor (r,c)
        def get(s):
            quot, rem = divmod(s-1, n)
            r = n-1-quot
            c = rem if r%2 != n%2 else n-1-rem
            return r, c
        
        queue = collections.deque([(1,0)])
        while queue:
            s, d = queue.popleft()
            if s == n*n: 
                return d
            for s2 in range(s+1, min(s+6, n*n)+1):
                r, c = get(s2)
                if board[r][c] != -1:
                    s2 = board[r][c]
                if s2 not in visited:
                    visited.add(s2)
                    queue.append((s2,d+1))
        return -1
```

## **Depth-First Search (DFS)**   
### 695. Max Area of Island
```python
class Solution(object):
    def maxAreaOfIsland(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        seen = set()
        def area(r, c):
            if not(0 <= r < len(grid) and 0 <= c < len(grid[0])) or (r,c) in seen or not grid[r][c]:
                return 0
            seen.add((r,c))
            return(1 + area(r-1, c) + area(r+1,c) + area(r, c-1) + area(r,c+1))
        
        return max(area(r, c)
                  for r in range(len(grid))
                  for c in range(len(grid[0])))
```
### 200. Number of Islands
```python
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        
        def dfs(r,c):
            
            if 0 <= r < len(grid) and 0 <= c < len(grid[0]) and grid[r][c] == "1":
                grid[r][c] = "0"
                dfs(r+1, c), dfs(r-1, c), dfs(r, c-1), dfs(r, c+1)
                return 1
            return 0
        
        return(sum(dfs(r, c)
                  for r in range(len(grid))
                  for c in range(len(grid[0]))))
```

### 547. Friend Circles
```python
class Solution:
    def findCircleNum(self, M: List[List[int]]) -> int:
        def dfs(i):
            seen[i] = 1
            for j in range(len(M)):
                if seen[j] == 0 and M[i][j] == 1:
                    dfs(j)
        
        seen = [0]*len(M)
        circle = 0
        for i in range(len(M)):
            if seen[i] == 0:
                circle += 1
                dfs(i)
        
        return circle
```

### 130. Surrounded Regions
```python
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        if not board or not board[0]:
            return
        
        r = len(board)
        c = len(board[0])
        
        def dfs(i, j):
            if not (0 <= i < r and 0 <= j < c):
                return
            if board[i][j] == 'O':
                #if not visited
                board[i][j] = '#'
                dfs(i+1, j), dfs(i-1, j), dfs(i, j+1), dfs(i, j-1)
        
        #search 'O' that are located at the boundary of the board
        for i in range(r):
            dfs(i, 0)
            dfs(i, c-1)
        for j in range(c):
            dfs(0, j)
            dfs(r-1, j)
        
        for i in range(r):
            for j in range(c):
                if board[i][j] == 'O':
                    board[i][j] = 'X'
                elif board[i][j] == '#':
                    board[i][j] = 'O'
```

### 417. Pacific Atlantic Water Flow
```python
class Solution:
    def pacificAtlantic(self, matrix: List[List[int]]) -> List[List[int]]:
        
        if not matrix or not matrix[0]:
            return []
            
        def dfs(visited,i,j):
            #water flow to this ocean
            visited[i][j] = 1
            for x,y in [(i+1, j), (i-1, j), (i, j-1), (i, j+1)]:
                if not(0 <= x < r and 0 <= y < c) or matrix[i][j] > matrix[x][y] or visited[x][y]:
                    continue
                dfs(visited, x, y)
                        
        r = len(matrix)
        c = len(matrix[0])
        result = []
        
        #use two matrix to keep track of water flow
        pacific = [[0 for i in range (c)]for j in range (r)]
        atlantic = [[0 for i in range(c)] for j in range(r)]

        for i in range(r):
            #water flow to pacific ocean
            dfs(pacific, i, 0)
            #water flow to atlantic ocean
            dfs(atlantic, i, c-1)
            
        for j in range(c):
            #water flow to pacific ocean
            dfs(pacific, 0, j)
            #water flow to atlantic ocean
            dfs(atlantic, r-1, j)
        
        for i in range(r):
            for j in range(c):
                if pacific[i][j] and atlantic[i][j]:
                    result.append([i,j])
        return result
```
