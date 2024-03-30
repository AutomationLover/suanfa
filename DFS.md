#DFS #2^n 

# Summary



## when using
- 树的分治和遍历，成对出现比如括号
- 不是只给解的数量 （DP 处理 解的数量）
- 2^n 问题

## how


参数：孩子需要从父亲了解什么

返回：父亲需要孩子了解什么

参数
- 递归出口
- 边界条件

步骤
- 画图
- 定参数
- 父子依赖关系
  - 如何进入下一层
  - 如何返回上一层

## template
```python

def dfs(node, visited):
    # 递归出口 (Base case or exit condition)
    if node is None: 
        return

    # 进入下一层要做什么 (What to do before entering the next level)
    # Process current node here.
    print(node.val)

    # 边界条件 (Boundary conditions)
    if node.left is not None:
        # Go to the left subtree
        dfs(node.left)

    if node.right is not None:
        # Go to the right subtree
        dfs(node.right)
```

## examples
重复选择元素 

    - 可以定义start， 但是i不能+1
    - 或者不定义start

```python
class Solution:
    def cherryPickup(self, grid: List[List[int]]) -> int:
        n, m = len(grid), len(grid[0])

        @functools.lru_cache(None)
        def dfs(x1, y1, x2, y2):
            if not (0 <= x1 < n and 0 <= y1 < m and 0 <= x2 < n and 0 <= y2 < m): # 越界，返回负无穷
                return -float('inf')
            if grid[x1][y1] == -1 or grid[x2][y2] == -1: # 走到障碍上，返回负无穷
                return -float('inf')
            res = 0
            if x1 != x2 or y1 != y2: # 两个人走到不同位置，把两个位置的樱桃都吃掉
                res += grid[x1][y1] + grid[x2][y2]
            elif grid[x1][y1] == 1: # 两个人走到相同位置，当前位置有樱桃，则只能吃到1个
                res += 1
            if x1 == n - 1 and y1 == m - 1 and x2 == n - 1 and y2 == m - 1: # 搜索的终止条件
                return res
            res += max(dfs(x1 + 1, y1, x2 + 1, y2),
                      dfs(x1 + 1, y1, x2, y2 + 1),
                      dfs(x1, y1 + 1, x2 + 1, y2),
                      dfs(x1, y1 + 1, x2, y2 + 1))
            return res
            
        return max(dfs(0, 0, 0, 0), 0) # 如果只能走到障碍上或越界那就会返回负无穷，所以要跟0取max
```
不重复选择元素

    - start设置为 i+1

```python
    for i in range(start, len(nums)):
        path.append(nums[i])
        backtrack(path, ans, i+1) # only use one time
        path.pop()

```

```python


def numIslands(grid):
    if not grid:
        return 0
    if not grid[0]:
        return 0
    max_row = len(grid)
    max_col = len(grid[0])
    water = '0'
    land = '1'
    def is_out_of_grid(i, j):
        if i < 0 or j<0:
            return True
        if i >= max_row or j>=max_col:
            return True
        return False

    def dfs(i, j):
        if is_out_of_grid(i,j) or grid[i][j]==water:
            return
        grid[i][j] = water
        dfs(i+1, j)
        dfs(i-1,j)
        dfs(i,j+1)
        dfs(i,j-1)

    result = 0
    for i in range(max_row):
        for j in range(max_col):
            if grid[i][j] == land:
                result += 1
                dfs(i,j)
    return result

def test():
    # Example 1
    grid1 = [
        ["1","1","1","1","0"],
        ["1","1","0","1","0"],
        ["1","1","0","0","0"],
        ["0","0","0","0","0"]
    ]
    #print(numIslands(grid1))  # Output: 1

    # Example 2
    grid2 = [
        ["1","1","0","0","0"],
        ["1","1","0","0","0"],
        ["0","0","1","0","0"],
        ["0","0","0","1","1"]
    ]
    print(numIslands(grid2))  # Output: 3
    
```

# Leetcode
- https://leetcode.cn/problems/combination-sum/description/
- https://leetcode.cn/problems/combination-sum-ii/description/
- https://leetcode.cn/problems/combination-sum-iii/description/
- https://leetcode.cn/problems/combination-sum-iv/  只要求解的个数(DP)
