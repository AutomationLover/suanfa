# name


## when using


## template


## examples
```python

# https://leetcode.cn/problems/evaluate-reverse-polish-notation/
# 150. 逆波兰表达式求值 - 力扣（LeetCode）

from operator import add, sub, mul
class Solution:
    op_map = {'+': add, '-': sub, '*': mul, '/': lambda x, y: int(x / y)}
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []
        for token in tokens:
            if token in self.op_map:
                val2 = stack.pop()
                val1 = stack.pop()
                stack.append(self.op_map[token](val1, val2))
            else:
                stack.append(int(token))
        return stack.pop()

```
