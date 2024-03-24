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