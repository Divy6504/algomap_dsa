# Sliding window-
This file contains all the solutions of the sliding window questions of algomap leetcode sheet.
Language used-C++

## 1.Maximum average subarray 1
**Link:** https://leetcode.com/problems/maximum-average-subarray-i/description/

class Solution 
{
public:
    double findMaxAverage(vector<int>& nums, int k)
    {
        int n=nums.size();
        int s=0;
        int e=0;
        double sum=0.0;
        double max_avg=INT_MIN;
        double avg;
        while(e<n)
        {
            sum+=nums[e];
            if((e-s+1)==k)
            {
                avg=sum/k;
                max_avg=max(max_avg,avg);
                sum-=nums[s];
                s++;
            }
            e++;
        }
        return max_avg;
    }
};



## 2.Maximum consecutive ones 3-
**Link:** https://leetcode.com/problems/max-consecutive-ones-iii/description/

class Solution 
{
public:
    int longestOnes(vector<int>& nums, int k) 
    {
         int s = 0, e = 0, zeros = 0, max_count = 0;
        int n = nums.size();
        while (e < n) 
        {
            if (nums[e] == 0) 
            zeros++;
            while (zeros > k) 
            {
                if (nums[s] == 0) 
                zeros--;
                s++;
            }
            max_count = max(max_count, e - s + 1);
            e++;
        }
        return max_count;
    }
};



## 3.Longest subtsring without repeating characters-
**Link:** https://leetcode.com/problems/longest-substring-without-repeating-characters/description/

class Solution 
{
public:
    int lengthOfLongestSubstring(string s) 
    {
        unordered_map<char,int>m;
        int st = 0, longest = 0, n = s.length();
    for (int e = 0; e < n; ++e) 
    {
        if (m.count(s[e]) && m[s[e]] > st) 
        {
            st = m[s[e]];
        }
        m[s[e]] = e + 1;
        longest = max(longest, e - st + 1);
    }
    return longest;
    }
};



## 4.Longest repeating character replacement-
**Link** https://leetcode.com/problems/longest-repeating-character-replacement/description/

class Solution 
{
public:
    int characterReplacement(string s, int k) 
    {
        int n = s.size();                  
        unordered_map<char,int> m;
        int st = 0, max_count = 0, result = 0;
        for (int e = 0; e < n; ++e) 
        {
            m[s[e]]++;
            max_count = max(max_count, m[s[e]]);  
            if (e - st + 1 - max_count > k) 
            {
                m[s[st]]--;
                st++;
            }
            result = max(result, e - st + 1);
        }
        return result;
    }
};



## 5.Minimum size subarray sum-
**Link:** https://leetcode.com/problems/minimum-size-subarray-sum/description/

class Solution 
{
public:
    int minSubArrayLen(int target, vector<int>& nums) 
    {
        int s = 0, e = 0, sum = 0;
        int min_count = INT_MAX;
        int n = nums.size();
        while (e < n) 
        {
            sum += nums[e];     
            while (sum >= target) 
            {
                min_count = min(min_count, e - s + 1);
                sum -= nums[s++];
            }
            e++;
        }
        return (min_count == INT_MAX) ? 0 : min_count;
    }
};



## 6.Permutation in string-
**Link:** https://leetcode.com/problems/permutation-in-string/description/

class Solution 
{
public:
    bool checkInclusion(string s1, string s2) 
    {
        int n1 = s1.length();
        int n2 = s2.length();
        if (n1 > n2) return false;
        vector<int> s1Counts(26, 0);
        vector<int> s2Counts(26, 0);
        for (int i = 0; i < n1; i++) 
        {
            s1Counts[s1[i] - 'a']++;
            s2Counts[s2[i] - 'a']++;
        }
        if (s1Counts == s2Counts) 
        return true;
        for (int i = n1; i < n2; i++) 
        {
            s2Counts[s2[i] - 'a']++;
            s2Counts[s2[i - n1] - 'a']--;
            if (s1Counts == s2Counts) 
            return true;
        }
        return false;
    }
};
