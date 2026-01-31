# Recursive backtracking-
This file contains all the solutions of the backtracking questions of algomap leetcode sheet.
Language used-C++

## 1.Subsets-
**Link:** https://leetcode.com/problems/subsets/description/

class Solution 
{
public:
void backtrack(int index,vector<int>&res,vector<vector<int>>&ans,vector<int>& nums)
{
    int n=nums.size();
    if(index==n)
    {
        ans.push_back(res);
        return ;
    }
     res.push_back(nums[index]);
        backtrack(index + 1, res, ans, nums);
        res.pop_back();
        backtrack(index + 1, res, ans, nums);
}
    vector<vector<int>> subsets(vector<int>& nums) 
    {
        vector<vector<int>>ans;
        vector<int>res;
        backtrack(0,res,ans,nums);
        return ans;
    }
};



## 2.Permutations-
**Link:** https://leetcode.com/problems/permutations/description/

class Solution 
{
public:
vector<vector<int>>result;
    void backtrack(vector<int>& nums, int index) 
    {
        if (index == nums.size()) 
        {
            result.push_back(nums);
            return;
        }
        for (int i = index; i < nums.size(); ++i) 
        {
            swap(nums[index], nums[i]);
            backtrack(nums, index + 1);
            swap(nums[index], nums[i]);
        }
    }
    vector<vector<int>> permute(vector<int>& nums) 
    {
        backtrack(nums, 0);
        return result;
    }
};



## 3.Combinations-
**Link:** https://leetcode.com/problems/combinations/description/

class Solution 
{
public:
vector<vector<int>> res;
    vector<int> path;
    void backtrack(int n, int k, int start) 
    {
        if (path.size() == k) 
        {
            res.push_back(path);
            return;
        }
        for (int i = start; i <= n; i++) 
        {
            path.push_back(i);
            backtrack(n, k, i + 1);
            path.pop_back();
        }
    }
    vector<vector<int>> combine(int n, int k) 
    {
        backtrack(n, k, 1);
        return res;
    }
};



## 4.Combination sum-
**Link:** https://leetcode.com/problems/combination-sum/description/

class Solution 
{
public:
vector<vector<int>> res;
    vector<int> ans;
    void backtrack(vector<int>& candidates, int target, int index, int sum) 
    {
        if (sum == target)
        {
            res.push_back(ans);
            return;
        }
        if (sum > target || index >= candidates.size())
        return;
        ans.push_back(candidates[index]);
        backtrack(candidates, target, index, sum + candidates[index]);
        ans.pop_back();
        backtrack(candidates, target, index + 1, sum);
    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) 
    {
        backtrack(candidates, target, 0, 0);
        return res;
    }
};



## 5.Letter combinations of a phone number-
**Link:** https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/

class Solution 
{
public:
 void backtrack(const string& digits, int index, string& path, vector<string>& res, const vector<string>& phoneMap) 
 {
        if (index == digits.size()) 
        {
            res.push_back(path);
            return;
        }
        string possibleLetters = phoneMap[digits[index] - '0'];
        for (char c : possibleLetters) 
        {
            path.push_back(c);               
            backtrack(digits, index + 1, path, res, phoneMap); 
            path.pop_back(); 
        }
 }
 vector<string> letterCombinations(string digits) 
    {
        if (digits.empty()) 
        return {};
        vector<string> res;
        string path;
        vector<string> phoneMap = 
        {
            "",     
            "",     
            "abc",  
            "def",  
            "ghi",  
            "jkl",  
            "mno",  
            "pqrs", 
            "tuv",  
            "wxyz"  
        };
        backtrack(digits, 0, path, res, phoneMap);
        return res;
    }
};



## 6.Generate parentheses-
**Link:** https://leetcode.com/problems/generate-parentheses/description/

class Solution 
{
public:
void backtrack(int openCount, int closeCount, int maxPairs, string& current, vector<string>& ans) 
{
        if (current.size() == maxPairs * 2) 
        {
            ans.push_back(current);
            return;
        }
        if (openCount < maxPairs) 
        {
            current.push_back('(');
            backtrack(openCount + 1, closeCount, maxPairs, current, ans);
            current.pop_back();
        }
        if (closeCount < openCount) 
        {
            current.push_back(')');
            backtrack(openCount, closeCount + 1, maxPairs, current, ans);
            current.pop_back();
        }
    }
    vector<string> generateParenthesis(int n) 
    {
        vector<string> ans;
        string current;
        backtrack(0, 0, n, current, ans);
        return ans;
    }
};



## 7.Word search-
**Link:** https://leetcode.com/problems/word-search/description/

class Solution 
{
public:
bool dfs(vector<vector<char>>& board, string& word, int i, int j, int idx) 
{
        if (idx == word.size()) return true;
        if (i < 0 || j < 0 || i >= board.size() || j >= board[0].size() || board[i][j] != word[idx]) 
            return false;
        char temp = board[i][j];
        board[i][j] = '#';
        bool found = dfs(board, word, i+1, j, idx+1) ||
                     dfs(board, word, i-1, j, idx+1) ||
                     dfs(board, word, i, j+1, idx+1) ||
                     dfs(board, word, i, j-1, idx+1);       
        board[i][j] = temp;
        return found;
}
    bool exist(vector<vector<char>>& board, string word) 
    {
       int m = board.size();
        int n = board[0].size();
        for (int i = 0; i < m; i++) 
        {
            for (int j = 0; j < n; j++) 
            {
                if (dfs(board, word, i, j, 0)) 
                {
                    return true;
                }
            }
        }
        return false;
    }
};



