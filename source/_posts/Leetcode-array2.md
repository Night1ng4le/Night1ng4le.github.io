---
title: Leetcode - Best Time to Buy and Sell Stock
categories: [Leetcode]
tags: [Array,动态规划]
---
### Problem link
https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/

### Description
Say you have an array for which the i<sup>th</sup> element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

<!--more-->

**Example 1:**
> **Input:** [7,1,5,3,6,4]
> **Output:** 5
> **Explanation:** Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
>
>  Not 7-1 = 6, as selling price needs to be larger than buying price.


**Example 2:**

> **Input:** [7,6,4,3,1]
> **Output:** 0
> **Explanation:** In this case, no transaction is done, i.e. max profit = 0.


### Solution

Version1
```c++
int maxProfit_k_any(int max_k, int[] prices) {
    int n = prices.length;
    if (max_k > n / 2) 
        return maxProfit_k_inf(prices);

    int[][][] dp = new int[n][max_k + 1][2];
    for (int i = 0; i < n; i++) 
        for (int k = max_k; k >= 1; k--) {
            if (i - 1 == -1) { 
                /* 处理 base case */
                dp[i][k][0] = 0;
                dp[i][k][1] = -prices[i];
                continue;
            }
            dp[i][k][0] = max(dp[i-1][k][0], dp[i-1][k][1] + prices[i]);
            dp[i][k][1] = max(dp[i-1][k][1], dp[i-1][k-1][0] - prices[i]);     
        }
    return dp[n - 1][max_k][0];
}

```


Loading...