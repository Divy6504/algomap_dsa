# Arrays & Strings-
This file contains all the solutions of the arrays and strings questions of algomap leetcode sheet.
Language used-C++

## 1.Find closest number to zero-
**Link:** https://leetcode.com/problems/find-closest-number-to-zero/description/

class Solution 
{
public:
    int findClosestNumber(vector<int>& nums) 
    {
        int clo=nums[0];
        for(int i=1;i<nums.size();i++)
        {
            if((abs(nums[i])<abs(clo))||(abs(nums[i])==abs(clo)&& nums[i]>clo))
            {
                clo=nums[i];
            }
        }
        return clo;
    }
};



## 2.Merge strings alternately-
**Link:** https://leetcode.com/problems/merge-strings-alternately/description/

class Solution 
{
public:
    string mergeAlternately(string word1, string word2) 
    {
        int j=0;
        string c="";
        if(word1.length()==word2.length())
        {
           for(int i=0;i<word1.length();i++) 
           {
            c+=word1[i];
            c+=word2[i];
           }
        }
        else if(word1.length()>word2.length())
        {
            for(int i=0;i<word2.length();i++)
            {
            c+=word1[i];
            c+=word2[i];      
            }
            for(int i=word2.length();i<word1.length();i++)
            {
                c+=word1[i];
            }
        }
        else
        {
            for(int i=0;i<word1.length();i++)
            {
            c+=word1[i];
            c+=word2[i]; 
            }
           for(int i=word1.length();i<word2.length();i++)
           {
            c+=word2[i];
           } 
        }
        return c;
    }
};


## 3.Roman To Integer-
**Link:** https://leetcode.com/problems/roman-to-integer/description/

class Solution 
{
public:
    int romanToInt(string s) 
    {
        unordered_map<string, int> twoChar =
         {
            {"IV", 4}, {"IX", 9},
            {"XL", 40}, {"XC", 90},
            {"CD", 400}, {"CM", 900}
        };
        unordered_map<char, int> oneChar = 
        {
            {'I', 1}, {'V', 5}, {'X', 10},
            {'L', 50}, {'C', 100}, {'D', 500}, {'M', 1000}
        };
        int res = 0;
        int i = 0;
        while (i < s.length())
        {
            if (i + 1 < s.length() && twoChar.count(s.substr(i, 2)))
             {
                res += twoChar[s.substr(i, 2)];
                i += 2;
            } 
            else 
            {
                res += oneChar[s[i]];
                i++;
            }
        }
        return res;
    }
};



## 4.Is Subsequence-
**Link:** https://leetcode.com/problems/is-subsequence/description/

class Solution
 {
public:
    bool isSubsequence(string s, string t) 
    {
        int j=0;
        for(int i=0;i<t.length()&&j<s.length();i++)
        {
            if(t[i]==s[j])
            j++;
        }
        if(j==s.size())
        return true;
        else
        return false;
    }
};



## 5. Best time to buy and sell stock-
**Link:** https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/

class Solution 
{
public:
    int maxProfit(vector<int>& prices) 
    {
        int minPrice = INT_MAX;
        int maxProfit = 0;
        for (int price : prices) 
        {
            minPrice = min(minPrice, price);
            maxProfit = max(maxProfit, price - minPrice);
        }
        return maxProfit;
    }
};



## 6.Longest common prefix-
**Link:** https://leetcode.com/problems/longest-common-prefix/description/

class Solution 
{
public:
    string longestCommonPrefix(vector<string>& strs) 
    {
        if (strs.empty()) 
        return "";
        for (int i = 0; i < strs[0].size(); ++i) 
        {
            char ch = strs[0][i];
            for (int j = 1; j < strs.size(); ++j) 
            {
                if (i >= strs[j].size() || strs[j][i] != ch)
                {
                    return strs[0].substr(0, i);
                }
            }
        }
        return strs[0]; 
    }
};



## 7.Summary ranges-
**Link:** https://leetcode.com/problems/summary-ranges/description/

class Solution 
{
public:
    vector<string> summaryRanges(vector<int>& nums) 
    {
        vector<string> ans;
        int n = nums.size();
        int i = 0;
        while (i < n) 
        {
            int start = nums[i];
            while (i < n - 1 && nums[i] + 1 == nums[i + 1]) 
            {
                i++;
            }
            if (start != nums[i]) 
            {
                ans.push_back(to_string(start) + "->" + to_string(nums[i]));
            } 
            else 
            {
                ans.push_back(to_string(nums[i]));
            }
            i++;
        }
        return ans;
    }
};



## 8.Product of array except self-
**Link:** https://leetcode.com/problems/product-of-array-except-self/description/

class Solution 
{
public:
    vector<int> productExceptSelf(vector<int>& nums) 
    {
        int n=nums.size();
        vector<int>ans(n,1);
        for(int i=1;i<n;i++)
        {
            ans[i]=ans[i-1]*nums[i-1];
        }
        int right=1;
        for(int i=n-1;i>=0;i--)
        {
            ans[i]*=right;
            right*=nums[i];
        }
        return ans;
    }
};



## 9.Merge Intervals-
**Link:** https://leetcode.com/problems/merge-intervals/description/

class Solution
{
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) 
    {
    vector<vector<int>> ans;
    if (intervals.empty()) 
    return ans;
    sort(intervals.begin(),intervals.end());
    vector<int>current=intervals[0];
    for (int i = 1; i < intervals.size(); i++) 
    {
        if (current[1] >= intervals[i][0]) 
        {
            current[1] = max(current[1], intervals[i][1]);
        } 
        else
        {
            ans.push_back(current);
            current = intervals[i];
        }
    }
    ans.push_back(current);
    return ans;
}
};
  


## 10.Spiral Matrix-
**Link:** https://leetcode.com/problems/spiral-matrix/description/

class Solution 
{
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) 
    {
        vector<int> ans;
        if (matrix.empty()) 
        return ans;
        int m = matrix.size();
        int n = matrix[0].size();
        int UP = 0, RIGHT = 1, DOWN = 2, LEFT = 3;
        int direction = RIGHT;
        int UP_WALL = 0;
        int RIGHT_WALL = n;
        int DOWN_WALL = m;
        int LEFT_WALL = -1;
        int i = 0,j = 0;
        while (ans.size() != m * n) 
        {
            if (direction == RIGHT) 
            {
                while (j < RIGHT_WALL) 
                {
                    ans.push_back(matrix[i][j]);
                    j++;
                }
                i++;
                j--;
                RIGHT_WALL--;
                direction = DOWN;
            } 
            else if (direction == DOWN) 
            {
                while (i < DOWN_WALL) 
                {
                    ans.push_back(matrix[i][j]);
                    i++;
                }
                i--;
                j--;
                DOWN_WALL--;
                direction = LEFT;
            } 
            else if (direction == LEFT) 
            {
                while (j > LEFT_WALL) 
                {
                    ans.push_back(matrix[i][j]);
                    j--;
                }
                i--;
                j++;
                LEFT_WALL++;
                direction = UP;
            } 
            else 
            {
                while (i > UP_WALL) 
                {
                    ans.push_back(matrix[i][j]);
                    i--;
                }
                i++;
                j++;
                UP_WALL++;
                direction = RIGHT;
            }
        }
        return ans;
    }
};



## 11.Rotate image-
**Link:** https://leetcode.com/problems/rotate-image/description/

class Solution 
{
public:
    void rotate(vector<vector<int>>& matrix) 
    {
        for(int i=0;i<matrix.size();i++)
        {
            for(int j=matrix.size()-1;j>=0;j--)
            {
                matrix[i].push_back(matrix[j][i]);
            }
        }
        for(auto& row:matrix)
        {
            int k=row.size();
            row.erase(row.begin(),row.begin()+k/2);
        }
        for(int i=0;i<matrix.size();i++)
        {
            for(int val:matrix[i])
            {
                cout<<val<<" "<<endl;
            }
        }
    }
};



