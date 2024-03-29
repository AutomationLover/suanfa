# name


## when using


## template
```python
    def __init__(self, n):
        self.parent = list(range(n))
    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]
```

## examples
```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.groups = n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x]) # Path compression
        return self.parent[x]

    def union(self, x, y):
        x_root = self.find(x)
        y_root = self.find(y)

        if x_root != y_root:
            self.parent[x_root] = y_root
            self.groups -= 1

    def connected(self, x, y):
        return self.find(x) == self.find(y)

def earliestAcq(logs, n):
    logs.sort()
    uf = UnionFind(n)

    for timestamp, x, y in logs:
        uf.union(x, y)
        if uf.groups == 1:
            return timestamp

    return -1

def test():
    # Example usage
    logs = [[20190101, 0, 1], [20190104, 3, 4], [20190107, 2, 3], [20190211, 1, 5], [20190224, 2, 4], [20190301, 0, 3], [20190312, 1, 2], [20190322, 4, 5]]
    n = 6
    print(earliestAcq(logs, n))  # Output: 20190301



```

```python

class UnionFind:
    def __init__(self, n):
        self.root = [i for i in range(n)]
        self.size = [1] * n
        self.part = n

    def find(self, x):
        if x != self.root[x]:
            root_x = self.find(self.root[x])
            self.root[x] = root_x
            return root_x
        return x

    def union(self, x, y):
        root_x = self.find(x)
        root_y = self.find(y)
        if root_x == root_y:
            return
        if self.size[root_x] >= self.size[root_y]:
            root_x, root_y = root_y, root_x
        self.root[root_x] = root_y
        self.size[root_y] += self.size[root_x]
        self.size[root_x] = 0
        self.part -= 1
        return

    def get_root_part(self):
        part = defaultdict(list)
        for i in range(len(self.root)):
            part[self.find(i)].append(i)
        return part


class Solution:
    def generateSentences(self, synonyms: List[List[str]], text: str) -> List[str]:
        words = []
        for lst in synonyms:
            words.extend(lst)
        words = list(set(words))
        ind = {word: i for i, word in enumerate(words)}
        n = len(ind)

        uf = UnionFind(n)
        for a, b in synonyms:
            uf.union(ind[a], ind[b])
        part = uf.get_root_part()
        for k in part:
            part[k].sort(key=lambda x: words[x])
            
        def dfs(i):
            if i == m:
                ans.append(" ".join(pre))
                return
            if lst[i] not in ind:
                pre.append(lst[i])
                dfs(i + 1)
                pre.pop()
            else:
                for j in part[uf.find(ind[lst[i]])]:
                    pre.append(words[j])
                    dfs(i + 1)
                    pre.pop()
            return

        lst = text.split(" ")
        m = len(lst)
        ans = []
        pre = []
        dfs(0)
        return ans
        
```