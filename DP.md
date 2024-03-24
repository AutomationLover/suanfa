# name


## when using


## template


## examples
```python
# Coin Change II
def change(amount, coins):
    dp = [0] * (amount + 1)
    dp[0] = 1

    for coin in coins:
        for i in range(coin, amount + 1):
            dp[i] += dp[i - coin]

    return dp[amount]

amount1 = 5
coins1 = [1, 2, 5]
print(change(amount1, coins1))  # Output: 4    
```

