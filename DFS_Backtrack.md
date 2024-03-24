#BFD #backtrack #2^n 

# Summary
Backtrack, 求排列组合所有方案 （DP 解的个数）
start+1 不重复元素


## when using
- 枚举所有可能的解
- 不是只给解的数量 （DP 处理 解的数量）
- 2^n 问题

## template
```python
def backtrack(candidate):
    if reject(candidate):
        return
    if accept(candidate):
        output(candidate)
    else:
        for next_candidate in list_of_candidates:
            add(next_candidate, candidate)
            backtrack(candidate)
            remove(next_candidate, candidate)
```

## examples
重复选择元素 

    - 可以定义start， 但是i不能+1
    - 或者不定义start
```python
def combinationSum(candidates, target):
    def backtrack(start, path, target):
        if target == 0:
            result.append(path[:])
            return
        for i in range(start, len(candidates)):
            if candidates[i] > target:
                continue
            path.append(candidates[i])
            backtrack(i, path, target - candidates[i])
            path.pop()
```
不重复选择元素

    - start设置为 i+1

```python
    for i in range(start, len(nums)):
        path.append(nums[i])
        backtrack(path, ans, i+1) # only use one time
        path.pop()

```

# Leetcode
- https://leetcode.cn/problems/combination-sum/description/
- https://leetcode.cn/problems/combination-sum-ii/description/
- https://leetcode.cn/problems/combination-sum-iii/description/
- https://leetcode.cn/problems/combination-sum-iv/  只要求解的个数(DP)