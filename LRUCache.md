# name


## when using


## template


## examples
```python
class LRUCache:
    def __init__(self, capacity):
        self.capacity = capacity
        self.cache = {}
        self.order = []

    def get(self, key):
        if key in self.cache:
            # Move the key to the end of the order list (most recently used)
            self.order.remove(key)
            self.order.append(key)
            return self.cache[key]
        else:
            return None

    def put(self, key, value):
        if key in self.cache:
            # Update the value and move the key to the end of the order list
            self.cache[key] = value
            self.order.remove(key)
            self.order.append(key)
        else:
            # Add the new key-value pair
            if len(self.cache) >= self.capacity:
                # Evict the least recently used item
                lru_key = self.order.pop(0)
                del self.cache[lru_key]
            self.cache[key] = value
            self.order.append(key)

# Example usage:
cache = LRUCache(2)
cache.put(1, 1)
cache.put(2, 2)
print(cache.get(1))  # Output: 1
cache.put(3, 3)       # evicts key 2
print(cache.get(2))  # Output: None
cache.put(4, 4)       # evicts key 1
print(cache.get(1))  # Output: None
print(cache.get(3))  # Output: 3
print(cache.get(4))  # Output: 4  
```

