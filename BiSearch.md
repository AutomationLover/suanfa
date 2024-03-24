# name


## when using


## template
Search Left
```python
def binary_search_left_most(arr, target):
    left = 0
    right = len(arr)
    
    while left < right - 1:
        mid = (left + right) // 2
        if arr[mid] < target:
            left = mid
        else:
            right = mid
    
    # Check the remaining two elements
    if arr[left] == target:
        return left
    elif arr[right] == target:
        return right
    else:
        return -1  # Not found
```

Search Right
```python
def binary_search_right_most(arr, target):
    left = 0
    right = len(arr)
    
    while left < right - 1:
        mid = (left + right) // 2
        if arr[mid] > target:
            right = mid
        else:
            left = mid
    
    # Check the remaining two elements
    if arr[right] == target:
        return right
    elif arr[left] == target:
        return left
    else:
        return -1  # Not
```



## examples
