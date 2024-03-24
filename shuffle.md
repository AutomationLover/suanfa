## example

```python
#shuffle
import random

class Solution:
    def __init__(self, nums):
        self.original = nums[:]  # Make a copy of the original array
        self.shuffled = nums[:]  # Initialize shuffled array with original array

    def reset(self):
        """
        Resets the array to its original configuration and returns it.
        """
        self.shuffled = self.original[:]
        return self.shuffled

    def shuffle(self):
        """
        Returns a random shuffling of the array.
        """
        for i in range(len(self.shuffled) - 1, 0, -1):
            j = random.randint(0, i)
            self.shuffled[i], self.shuffled[j] = self.shuffled[j], self.shuffled[i]
        return self.shuffled

# Example usage
nums = [1, 2, 3]
obj = Solution(nums)
print("Original array:", obj.original)  # Output: Original array: [1, 2, 3]

print("Shuffled array:", obj.shuffle())  # Output: Shuffled array: [2, 1, 3] (random)
print("Reset array:", obj.reset())  # Output: Reset array: [1, 2, 3]
print("Shuffled array:", obj.shuffle())  # Output: Shuffled array: [3, 2, 1] (random)

```