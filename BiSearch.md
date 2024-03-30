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
```python
def findMedianSortedArrays(shortNums, longNums):
    if len(shortNums) > len(longNums):
        shortNums, longNums = longNums, shortNums

    x, y = len(shortNums), len(longNums)
    start = 0
    end = x
    while start <= end:
        partitionX = (start + end) // 2
        partitionY = (x + y + 1) // 2 - partitionX

        maxLeftX = float('-inf') if partitionX == 0 else shortNums[partitionX - 1]
        minRightX = float('inf') if partitionX == x else shortNums[partitionX]

        maxLeftY = float('-inf') if partitionY == 0 else longNums[partitionY - 1]
        minRightY = float('inf') if partitionY == y else longNums[partitionY]

        if maxLeftX <= minRightY and maxLeftY <= minRightX:
            if (x + y) % 2 == 0:
                return (max(maxLeftX, maxLeftY) + min(minRightX, minRightY)) / 2.0
            else:
                return max(maxLeftX, maxLeftY)

        elif maxLeftX > minRightY:
            end = partitionX - 1
        else:
            start = partitionX + 1

    raise Exception("Input arrays are not sorted")

```