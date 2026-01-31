# Dynamic programming-
This file contains all the solutions of the dp questions of algomap leetcode sheet.
Language used-C++

## 1.Fibonacci number-
**Link:** https://leetcode.com/problems/Fibonacci-Number/description/

class Solution 
{
public:
int fib2(int n,int *arr)
{
    if(n==0 || n==1)
    return n;
    if(arr[n]!=0)
    return arr[n];
    int out=fib2(n-1,arr)+fib2(n-2,arr);
    arr[n]=out;
    return out;
}
    int fib(int n) 
    {
        int *arr=new int[n+1];
        for(int i=0;i<=n;i++)
        {
            arr[i]=0;
        }
        return fib2(n,arr);
    }
};



## 2.Climbing stairs-
**Link:** https://leetcode.com/problems/climbing-stairs/description/

class Solution 
{
public:
    int climbStairs(int n) 
    {
        int dp[n+1];
        dp[0]=1;
        dp[1]=1;
        for(int i=2;i<=n;i++)
        {
            dp[i]=dp[i-1]+dp[i-2];
        }
        return dp[n];
    }
};



## 3.Min cost climbing stairs-
**Link:** https://leetcode.com/problems/min-cost-climbing-stairs/description/

class Solution 
{
public:
    vector<int> dp;
    int mincost(vector<int>& cost, int n) 
    {
        if (n == 0 || n == 1)
            return 0;
        if (dp[n] != -1)
            return dp[n];
        int one = mincost(cost, n - 1) + cost[n - 1];
        int two = mincost(cost, n - 2) + cost[n - 2];
        return dp[n] = min(one, two);
    }
    int minCostClimbingStairs(vector<int>& cost) 
    {
        int n = cost.size();
        dp.assign(n + 1, -1);
        return mincost(cost, n);
    }
};



## 4.House robber-
**Link:** https://leetcode.com/problems/house-robber/description/

class Solution 
{
public:
    int rob(vector<int>& nums) 
    {
        int n=nums.size();
       vector<int>dp(n+1);
       if(n>1)
       {
       dp[0]=0;
       dp[1]=nums[0];
       dp[2]=nums[1];
       for(int i=2;i<n;i++)
       {
        dp[i+1]=max(dp[i-1]+nums[i],dp[i-2]+nums[i]);
       } 
       return max(dp[n],dp[n-1]);
       }
       return nums[0];
    }
};



## 5.Unique paths-
**Links:** https://leetcode.com/problems/unique-paths/description/

class Solution 
{
public:
    int uniquePaths(int m, int n) 
    {
        vector<vector<int>>dp(m,vector<int>(n,1));
        for(int i=1;i<m;i++)
        {
            for(int j=1;j<n;j++)
            {
                dp[i][j]=dp[i-1][j]+dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
};



## 6.Coin change-
**Link:** https://leetcode.com/problems/coin-change/description/

class Solution 
{
public:
    int coinChange(vector<int>& coins, int amount) 
    {
        vector<int> dp(amount + 1, amount + 1);
        dp[0] = 0;
        for (int i = 1; i <= amount; i++) 
        {
            for (int coin : coins) 
            {
                if (coin <= i) 
                {
                    dp[i] = min(dp[i], 1 + dp[i - coin]);
                }
            }
        }
        return (dp[amount] > amount) ? -1 : dp[amount];
    }
};



## 7.Longest increasing subsequence-
**Link:** https://leetcode.com/problems/longest-increasing-subsequence/description/

class Solution 
{
public:
    int lengthOfLIS(vector<int>& nums) 
    {
        int n = nums.size();
        vector<int> dp(n, 1);
        int ans = 1;
        for (int i = 0; i < n; i++) 
        {
            for (int j = 0; j < i; j++) 
            {
                if (nums[j] < nums[i]) 
                {
                    dp[i] = max(dp[i], dp[j] + 1);
                }
            }
            ans = max(ans, dp[i]);
        }
        return ans;
    }
};


