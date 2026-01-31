# Binary Search-
This file contains all the solutions of the binary search questions of algomap leetcode sheet.
Language used-C++

## 1.Binary Search-
**Link:** https://leetcode.com/problems/binary-search/description/

class Solution 
{
public:
    int search(vector<int>& nums,int target) 
    {
        int start=0;
        int end=nums.size()-1;
        while(start<=end)
        {
            int mid=start+(end-start)/2;
            if(nums[mid]>target)
            {
                end=mid-1;
            }
            else if(nums[mid]<target)
            {
                start=mid+1;
            }
            else
            {
                return mid;
            }
        }
        return -1;
    }
};



## 2.Search insert position-
**Link:** https://leetcode.com/problems/search-insert-position/description/ 

class Solution 
{
public:
    int searchInsert(vector<int>& nums, int target) 
    {
        int s=0;
        int e=nums.size()-1;
        while(s<=e)
        {
            int mid=s+(e-s)/2;
            if(nums[mid]>target)
            {
                e=mid-1;
            }
            else if(nums[mid]<target)
            {
                s=mid+1;
            }
            else if(nums[mid]==target)
            {
               return mid;
            }
        }
    return s;
    }
};



## 3.First bad version-
**Link:** https://leetcode.com/problems/first-bad-version/description/

class Solution 
{
public:
    int firstBadVersion(int n) 
    {
        int s=1;
        int e=n;
        while(s<=e)
        {
            int mid=s+(e-s)/2;
            if(isBadVersion(mid)==false && isBadVersion(mid+1)==true)
            {
                return mid+1;
            }
            else if(isBadVersion(mid)==false)
            {
                s=mid+1;
            }
            else if(isBadVersion(mid)==true)
            {
                if(mid==1)
                return mid;
                e=mid-1;
            }
        }
        return n;
    }
};



## 4.Valid perfect square-
**Link:** https://leetcode.com/problems/valid-perfect-square/description/

class Solution 
{
public:
    bool isPerfectSquare(int num) 
    {
        if (num < 1) 
        return false;
        long long start = 1, end = num;
        while (start <= end) 
        {
            long long mid = start + (end - start) / 2;
            long long sq = mid * mid;
            if (sq == num) 
                return true;
            else if (sq < num) 
                start = mid + 1;
            else 
                end = mid - 1;
        }
       return false;
    }
};



## 5.Search a 2d matrix-
**Link:** https://leetcode.com/problems/search-a-2d-matrix/description/

class Solution 
{
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) 
    {
        vector<int>v;
       for(int i=0;i<matrix.size();i++)
       {
        for(int j=0;j<matrix[0].size();j++)
        {
            v.push_back(matrix[i][j]);
        }
       }
       int s=0;
       int e=v.size()-1;
       while(s<=e)
       {
        int mid=s+(e-s)/2;
        if(v[mid]>target)
        {
            e=mid-1;
        }
        else if(v[mid]<target)
        {
            s=mid+1;
        }
        else if(v[mid]==target)
        {
            return true;
        }
       }
       return false;
    }
};



## 6.Find minimum in rotated sorted array-
**Link:** https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/

class Solution 
{
public:
        int findMin(vector<int>& nums)
        {
    int left = 0, right = nums.size() - 1;
    while (left < right) 
    {
        int mid = left + (right - left) / 2;
        if (nums[mid] > nums[right]) 
        {
            left = mid + 1; 
        }
         else 
        {
            right = mid; 
        }
    }
    return nums[left]; 
    }
};



## 7.Search in rotated sorted array-
**Link:** https://leetcode.com/problems/search-in-rotated-sorted-array/description/

class Solution 
{
public:
    int search(vector<int>& nums, int target) 
    {
        int left = 0, right = nums.size() - 1;
        while (left <= right) 
        {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) 
            return mid;
            if (nums[left] <= nums[mid]) 
            {
                if (nums[left] <= target && target < nums[mid])
                    right = mid - 1;
                else
                    left = mid + 1;
            }
            else 
            {
                if (nums[mid] < target && target <= nums[right])
                    left = mid + 1;
                else
                    right = mid - 1;
            }
        }
        return -1;
    }
};



## 8.Koko eating bananas-
**Link:** https://leetcode.com/problems/koko-eating-bananas/description/

class Solution 
{
public:
    int minEatingSpeed(vector<int>& piles, int h) 
    {
        int left = 1;
        int right =*max_element(piles.begin(), piles.end());
        while (left < right) 
        {
            int mid = left + (right - left) / 2;
            if (canFinish(piles, h, mid)) 
            {
                right = mid;
            } 
            else 
            {
                left = mid + 1;
            }
        }
        return left;
    }
private:
    bool canFinish(const vector<int>& piles, int h, int k) 
    {
        int hours = 0;
        for (int pile : piles) 
        {
            hours+=ceil(static_cast<double>(pile) / k);
        }
        return hours <= h;
    }
};