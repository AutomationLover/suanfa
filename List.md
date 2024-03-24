# name


## when using


## template


## examples
```python
# 接雨水
# 输入：height = [0,1,0,2,1,0,1,3,2,1,2,1]
# 输出：6
# 解释：上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 

def trap(height):
    if not height:
        return 0
    n = len(height)
    left_max = [0] * n
    right_max = [0] * n
    left_max[0] = height[0]
    right_max[n-1] = height[n-1]

    for i in range(1, n):
        left_max[i] = max(left_max[i-1], height[i])
        right_max[-i-1] = max(right_max[-i], height[-i-1])

    result = 0
    for i in range(1, n-1):
        water = min(left_max[i], right_max[i]) - height[i]
        result += water

    return result


```


```python
# Meeting Room
def merge_intervals(intervals):
    if not intervals:
        return []
    left = 0
    right = 1
    intervals.sort(key=lambda x: x[left])
    # sorted_intervals = sorted(intervals, key=lambda x: x[0])
    merged = [intervals[0]]

    for interval in intervals[1:]:
        last_merged = merged[-1]
        if interval[left] <= last_merged[right]:  # overlapped, updated right
            last_merged[right] = max(last_merged[right], interval[right])
        else:  # no overlap
            merged.append(interval)

    return merged

def test():
    # Test the function with examples
    intervals1 = [[1,3],[2,6],[8,10],[15,18]]
    intervals2 = [[1,4],[4,5]]

    print(merge_intervals(intervals1))  # Output: [[1,6],[8,10],[15,18]]
    print(merge_intervals(intervals2))  # Output: [[1,5]]

```

```python
import heapq

def minMeetingRooms(intervals):
    if not intervals:
        return 0

    end_times = []
    intervals.sort(key=lambda x: x[0])
    heapq.heappush(end_times, intervals[0][1])
    
    for i in range(1, len(intervals)):
        new_meeting_start = intervals[i][0]
        earliest_end = end_times[0]
        if new_meeting_start >= earliest_end:
            heapq.heappop(end_times)
        heapq.heappush(end_times, intervals[i][1])

    return len(end_times)
```


```python
def max_subarray_sum(nums):
    max_sum = nums[0]
    current_sum = nums[0]

    for num in nums[1:]:
        current_sum = max(num, current_sum + num)
        max_sum = max(max_sum, current_sum)

    return max_sum

# Test cases
nums1 = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
print(max_subarray_sum(nums1))  # Output: 6

nums2 = [1]
print(max_subarray_sum(nums2))  # Output: 1

nums3 = [5, 4, -1, 7, 8]
print(max_subarray_sum(nums3))  # Output: 23

```

```python
def productExceptSelf(nums):
    n = len(nums)
    left_products = [1] * n
    right_products = [1] * n
    output = [1] * n

    # Calculate the product of all elements to the left of each element
    for i in range(1, n):
        left_products[i] = left_products[i - 1] * nums[i - 1]

    # Calculate the product of all elements to the right of each element
    for i in range(n - 2, -1, -1):
        right_products[i] = right_products[i + 1] * nums[i + 1]

    # Multiply the left and right products to get the final result
    for i in range(n):
        output[i] = left_products[i] * right_products[i]

    return output

# Test the function with examples
print(productExceptSelf([1, 2, 3, 4]))  # Output: [24, 12, 8, 6]
print(productExceptSelf([-1, 1, 0, -3, 3]))  # Output: [0, 0, 9, 0, 0]

```