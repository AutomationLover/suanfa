# name
BFD

## when using


## template
```python
def find_nodes_by_bfd(node):
    queue = collections.deque([node])
    visited = set([node])
    while queue:
        cur_node = queue.popleft()
        for neighbor in cur_node.neighbors:
            if neighbor in visited:  # or 其他不满足条件
                continue
            
            visited.add(neighbor)
            queue.append(neighbor)
    return list(visited)
```

by layer

```python
def find_nodes_by_bfd_by_layer(node):
    queue = collections.deque([node])
    visited = set([node])
    while queue:
        for _ in range(len(queue)):
            cur_node = queue.popleft()
            for neighbor in cur_node.neighbors:
                if neighbor in visited:  # or 其他不满足条件
                    continue
                visited.add(neighbor)
                queue.append(neighbor)
    return list(visited)
```

short path first
Heapq 代替 deque，当边权重不一样的时候 Short Path First

```python
def modernLudo(length, graph):
    queue = [(0, 1)]
    distance = {
        i: float('-inf')
        for i in range(1, length + 1)
    }
    distance[1] = 0
    while queue:
        dist, node = heapq.heappop(queue)
        for next_node in graph[node]:
            if distance[next_node] > dist:
                distance[next_node] = dist
                heapq.heappush(queue, (dist, next_node))
        for next_node in range(node + 1, min(node + 7, length + 1)):
            if distance[next_node] > dist + 1:
                distance[next_node] = dist + 1
                heapq.heappush(queue, (dist + 1, next_node))
    return distance[length]
    
```



## examples
```python
from collections import defaultdict

def canFinish(numCourses, prerequisites):
    # Create a graph representation
    graph = defaultdict(list)
    in_degree = [0] * numCourses
    for course, prereq in prerequisites:
        graph[prereq].append(course)
        in_degree[course] += 1

    # Find courses with no prerequisites
    queue = [course for course in range(numCourses) if in_degree[course] == 0]

    # Perform topological sort
    count = 0
    while queue:
        course = queue.pop(0)
        count += 1
        for neighbor in graph[course]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)

    # If count is equal to numCourses, it means all courses can be completed
    return count == numCourses

def test():
    print(canFinish(2, [[1, 0]]))  # True
    print(canFinish(2, [[1, 0], [0, 1]]))  # False


```