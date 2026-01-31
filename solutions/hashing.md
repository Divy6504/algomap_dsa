# 1.Hashing-
This file contains all the solutions of the hashmaps and sets questions of algomap leetcode sheet.
Language used-C++

## 1.Jewels and stones-
**Link:** https://leetcode.com/problems/jewels-and-stones/description/

class Solution 
{
public:
    int numJewelsInStones(string jewels, string stones) 
    {
       unordered_set<char>s(jewels.begin(),jewels.end());
        int count=0;
        for(char c:stones)
        {
        if(s.count(c))
        {
            count++;
        }
        }
        return count;
    }
};



## 2.Contains duplicates-
**Link:** https://leetcode.com/problems/contains-duplicate/description/

class Solution 
{
public:
    bool containsDuplicate(vector<int>& nums) 
    {
        unordered_set<int>s;
        for(int c:nums)
        {
            if(s.count(c))
            {
                return true;
            }
            s.insert(c);
        }
      return false;
    }
};



## 3. Ransom note-
**Link:** https://leetcode.com/problems/ransom-note/description/

class Solution 
{
public:
    bool canConstruct(string ransomNote, string magazine) 
    {
        unordered_map<char,int>m;
        for(char c:magazine)
        {
            m[c]++;
        }
        for(char c:ransomNote)
        {
            if(m[c]==0)
            return false;
            m[c]--;
        }
        return true;
    }
};



## 4.Valid anagram-
**Link:** https://leetcode.com/problems/valid-anagram/description/

class Solution 
{
public:
    bool isAnagram(string s, string t) 
    {
        unordered_map<char,int>m;
        if(t.length()==s.length())
        {
        for(char c:s)
        {
            m[c]++;
        }
        for(char c:t)
        {
            if(m[c]==0)
            {
                return false;
            }
            m[c]--;
        }
        }
        else
        { 
        return false;
        }
        return true;
    }
};



## 5.Maximum number of balloons-
**Link:** https://leetcode.com/problems/maximum-number-of-balloons/description/

class Solution 
{
public:
    int maxNumberOfBalloons(string text) 
    {
        string balloon;
        unordered_map<char,int>m;
        for(char c:text)
        {
            m[c]++;
        }
        
            int count_b=m['b'];
            int count_a=m['a'];
            int count_l=m['l']/2;
            int count_o=m['o']/2;
            int count_n=m['n'];
        return min({count_b,count_a,count_l,count_o,count_n});
    }
};



## 6.Two sum-
**Link** https://leetcode.com/problems/two-sum/description/

class Solution 
{
public:
    int maxNumberOfBalloons(string text) 
    {
        string balloon;
        unordered_map<char,int>m;
        for(char c:text)
        {
            m[c]++;
        }
        
            int count_b=m['b'];
            int count_a=m['a'];
            int count_l=m['l']/2;
            int count_o=m['o']/2;
            int count_n=m['n'];
        return min({count_b,count_a,count_l,count_o,count_n});
    }
};



## 7.Valid sudoku-
**Link:** https://leetcode.com/problems/valid-sudoku/description/

class Solution 
{
public:
    bool isValidSudoku(vector<vector<char>>& board) 
    {
        unordered_map<char,int>m;
        char c,d;
        for(int i=0;i<board.size();i++)
        {
            m.clear();
            for(int j=0;j<board[0].size();j++)
            {
                c=board[i][j];
                if(c>'0'&& c<='9')
                {
                    if(m.count(c))
                    {
                        return false;
                    }
                    m[c]=j;
                }
            }
        }
        for(int i=0;i<board.size();i++)
        {
            m.clear();
            for(int j=0;j<board[0].size();j++)
            {
                d=board[j][i];
                if(d>'0'&& d<='9')
                {
                    if(m.count(d))
                    {
                        return false;
                    }
                    m[d]=j;
                }
            }
        }
        for (int boxRow = 0; boxRow < 9; boxRow += 3)
        {
            for (int boxCol = 0; boxCol < 9; boxCol += 3)
            {
                m.clear();
                for (int i = 0; i < 3; i++)
                {
                    for (int j = 0; j < 3; j++)
                    {
                        char ch = board[boxRow + i][boxCol + j];
                        if (ch != '.')
                        {
                            if (m.count(ch)) 
                            return false;
                            m[ch]=j;
                        }
                    }
                }
            }
        }
        return true;
    }
};



## 8.Group anagrams-
**Link:** https://leetcode.com/problems/group-anagrams/description/

class Solution 
{
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) 
    {
        unordered_map<string, vector<string>> anagramGroups;
        for (string word : strs) 
        {
            string sortedWord = word;
            sort(sortedWord.begin(), sortedWord.end());
            anagramGroups[sortedWord].push_back(word);
        }
        vector<vector<string>> result;
        for (auto& group : anagramGroups) 
        {
            result.push_back(group.second);
        }
        return result;
    }
};



## 9.Majority element-
**Link:** https://leetcode.com/problems/majority-element/description/

class Solution 
{
public:
    int majorityElement(vector<int>& nums) 
    {
        unordered_map<int,int>m;
        for(int i:nums)
        {
            m[i]++;
        }
        for(auto& j:m)
        {
            if(j.second>nums.size()/2.0)
            return j.first;
        }
        return 0;
    }
};



## 10.Longest consecutive subsequence-
**Link** https://leetcode.com/problems/longest-consecutive-sequence/description/

class Solution 
{
public:
    int longestConsecutive(vector<int>& nums) 
    {
        unordered_set<int>set(nums.begin(), nums.end());
        int longest = 0;
        for (int num : set) 
        {
            if (set.find(num - 1) == set.end()) 
            {
                int length = 1;
                int nextNum = num + 1;
                while (set.find(nextNum) != set.end()) 
                {
                    length++;
                    nextNum++;
                }
                longest = max(longest, length);
            }
        }
        return longest;
    }
};