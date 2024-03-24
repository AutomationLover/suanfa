# name


## when using


## template


## examples

```python
def maxSlidingWindow(nums, k):
    if not nums:
        return []
    
    result = []
    window = deque()
    
    for i in range(len(nums)):
        # remove elements outside of the window's range
        while window and window[0] < i - k + 1:
            window.popleft()
        
        # remove elements smaller than the current element from the back of the window
        while window and nums[i] >= nums[window[-1]]:
            window.pop()
        
        window.append(i)
        
        # add the maximum element to the result when the window is fully formed
        if i >= k - 1:
            result.append(nums[window[0]])
    
    return result
```

```python

def longest_palindromic_substring(s: str) -> str:
    if len(s) < 1:
        return ""

    start = 0
    end = 0

    for i in range(len(s)):
        len1 = expand_around_center(s, i, i)
        len2 = expand_around_center(s, i, i + 1)
        max_len = max(len1, len2)

        if max_len > end - start:
            start = i - (max_len - 1) // 2
            end = i + max_len // 2

    return s[start:end+1]

def expand_around_center(s: str, left: int, right: int) -> int:
    while left >= 0 and right < len(s) and s[left] == s[right]:
        left -= 1
        right += 1

    return right - left - 1

def test():
    # Test cases
    print(longest_palindromic_substring("babad"))  # Output: "aba" or "bab"
    print(longest_palindromic_substring("cbbd"))   # Output: "bb"

```
