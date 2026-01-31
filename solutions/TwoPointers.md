# Two pointers-
This file contains all the solutions of the two pointers questions of algomap leetcode sheet.
Language used-C++

## 1.Squares of a sorted array-
**Link:** https://leetcode.com/problems/squares-of-a-sorted-array/description/

class Solution 
{
public:
    vector<int> sortedSquares(vector<int>& nums) 
    {
        int n = nums.size();
        vector<int> result(n);
        int left = 0, right = n - 1;
        int pos = n - 1;
        while (left <= right) 
        {
            int leftSq = nums[left] * nums[left];
            int rightSq = nums[right] * nums[right];
            if (leftSq > rightSq) 
            {
                result[pos--] = leftSq;
                left++;
            }
             else 
            {
                result[pos--] = rightSq;
                right--;
            }
        }
        return result;
    }
};



## 2.Reverse string-
**Link:** https://leetcode.com/problems/reverse-string/description/

class Solution 
{
public:
    void reverseString(vector<char>& s) 
    {
        int left=0;
        int right=s.size()-1;
        while(left<right)
        {
            swap(s[left],s[right]);
            left++;
            right--;
        }
        for(int i=0;i<s.size()-1;i++)
        {
            cout<<s[i]<<endl;
        }
    }
};



## 3.Two sum 2-input array is sorted-
**Link** https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/

class Solution 
{
public:
    vector<int> twoSum(vector<int>& numbers, int target) 
    {
        vector<int>ans;
        int n=numbers.size();
        int l=0;
        int r=n-1;
        while(l<=r)
        {
            int sum=numbers[l]+numbers[r];
            if(sum==target)
            {
                ans.push_back(l+1);
                ans.push_back(r+1);
                break;
            }
            else if(sum>target)
            {
                r--;
            }
            else
            {
                l++;
            }
        }
        return ans;
    }
};



## 4.Valid palindrome-
**Link:** https://leetcode.com/problems/valid-palindrome/description/

class Solution 
{
public:
    bool isPalindrome(string s) 
    {
       s.erase(remove_if(s.begin(), s.end(), [](char c){ return !isalnum(c);}),s.end());
       for(char& c:s)
       {
        if(isupper(c))
        {
            c=tolower(c);
        }
       }
       int n=s.size();
       int l=0;
       int r=n-1;
       while(l<r)
       {
        if(s[l]==s[r])
        {
            l++;
            r--;
        }
        else
        {
            return false;
        }
       }
       return true;
    }
};


## 5.3Sum-
**Link:** https://leetcode.com/problems/3sum/description/

class Solution
{
public:
    vector<vector<int>> threeSum(vector<int>& nums) 
    {
        vector<vector<int>>ans;
        sort(nums.begin(),nums.end());
        int n=nums.size();
        for(int i=0;i<n-2;i++)
        {
        if(i>0 && nums[i]==nums[i-1])
        continue;
        int x=nums[i];
        int l=i+1;
        int r=n-1;
        while(l<r)
        {
            int y=nums[l];
            int z=nums[r];
            int sum=x+y+z;
            if(sum==0)
            {
               ans.push_back({x,y,z});
               while(l<r && nums[l]==nums[l+1])
               l++;
               while(l<r && nums[r]==nums[r-1])
               r--;
               l++;
               r--;
            }
            else if(sum<0)
            {
                l++;
            }
            else if(sum>0)
            {
                r--;
            }
        }
        }
        return ans;
    }
};



## 6.Container with most water-
**Link:** https://leetcode.com/problems/container-with-most-water/description/

class Solution 
{
public:
    int maxArea(vector<int>& height) 
    {
        int n=height.size();
        int l=0;
        int r=n-1;
        int max_area=0;
        while(l<r)
        {
            int diff=r-l;
            int h_diff=min(height[l],height[r]);
            int area=h_diff*diff;
            max_area=max(max_area,area);
            if(height[l]<height[r])
            {
                l++;
            }
            else
            {
                r--;
            }
        }
        return max_area;
    }
};

