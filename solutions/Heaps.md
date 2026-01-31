# Heaps-
This file contains all the solutions of the heap questions of algomap leetcode sheet.
Language used-C++

## 1.Last stone weight-
**Link:** https://leetcode.com/problems/last-stone-weight/description/

class Solution 
{
public:
    int lastStoneWeight(vector<int>& stones) 
    {
        int a,b;
        priority_queue<int>pq(stones.begin(),stones.end());
        while(pq.size()>1)
        {
            a=pq.top();
            pq.pop();
            b=pq.top();
            pq.pop();
            if(a!=b)
            {
            a=a-b;
            pq.push(a);
            }
        }
        if(!pq.empty())
        return pq.top();
        return 0;
    }
};



## 2.Kth largest element in an array-
**Link:** https://leetcode.com/problems/kth-largest-element-in-an-array/description/

class Solution 
{
public:
    int findKthLargest(vector<int>& nums, int k) 
    {
        priority_queue<int>pq(nums.begin(),nums.end());
        for(int i=0;i<k-1;i++)
        {
            pq.pop();
        }
        return pq.top();
    }
};



## 3.K closest points to origin-
**Link:** https://leetcode.com/problems/k-closest-points-to-origin/description/

class Solution 
{
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) 
    {
        priority_queue<pair<int, vector<int>>> pq;        
        for (auto &p : points) 
        {
            int dist = p[0]*p[0] + p[1]*p[1];
            pq.push({dist, p});
            if (pq.size() > k) 
            {
                pq.pop();
            }
        }
        vector<vector<int>> ans;
        while (!pq.empty()) 
        {
            ans.push_back(pq.top().second);
            pq.pop();
        }
        return ans;
    }
};


