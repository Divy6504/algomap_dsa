# Stacks-
This file contains all the solutions of the stacks questions of algomap leetcode sheet.
Language used-C++

## 1.Baseball game-
**Link:** https://leetcode.com/problems/baseball-game/description/

class Solution 
{
public:
    int calPoints(vector<string>& operations) 
    {
     stack<int>s;
     for(string op:operations)
     {
        if(op=="C")
        {
            s.pop();
        }
        else if(op=="D")
        {
            s.push(2*s.top());
        }
        else if(op=="+")
        {
            int top1=s.top();
            s.pop();
            int top2=s.top();
            s.push(top1);
            s.push(top1+top2);
        }
        else
        {
            s.push(stoi(op));
        }
     }
     int sum=0;
     while(!s.empty())
     {
        sum+=s.top();
        s.pop();
     }
     return sum;
    }
};



## 2.Valid parentheses-
**Link:** https://leetcode.com/problems/valid-parentheses/description/

class Solution 
{
public:
    bool isValid(string s) 
    {
        stack<char>st;
        for(int i=0;i<s.size();i++)
        {
            if(s[i]=='('||s[i]=='['||s[i]=='{')
            {
                st.push(s[i]);
            }
            else
            {
                if(st.empty())
                return false;
                else if(s[i]==')')
                {
                    if(st.top()=='(')
                     st.pop();
                     else
                     return false;
                }
            else if(s[i]==']')
            {
                if(st.top()=='[')
                  st.pop();
                  else
                  return false;
            }
            else if(s[i]=='}')
            {
                if(st.top()=='{')
                st.pop();
                else
                return false;
            }
            }
        }
        if(st.empty())
        return true;
        else 
        return false;
    }
};



## 3.Evaluate reverse polish notation-
**Link** https://leetcode.com/problems/evaluate-reverse-polish-notation/description/

class Solution
{
public:
    int evalRPN(vector<string>& tokens) 
    {
        stack<int>s;
        int top2;
        int top1;
        for(string st:tokens)
        {
            if(st=="+"||  st=="-"||st=="*"||st=="/")
            {
                top1=s.top();
                s.pop();
                top2=s.top();
                s.pop();
            }
            if(st=="+")
            s.push(top2+top1);
            else if(st=="-")
            s.push(top2-top1);
            else if(st=="*")
            s.push(top2*top1);
            else if(st=="/")
            s.push(top2/top1);
            else
            s.push(stoi(st));
        }
        return s.top();
    }
};



## 4.Daily temperatures-
**Link:** https://leetcode.com/problems/daily-temperatures/description/

class Solution 
{
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) 
    {
        int n = temperatures.size();
        vector<int> ans(n, 0);
        stack<int> st; 
        for (int i = n - 1; i >= 0; i--) 
        {
            while (!st.empty() && temperatures[st.top()] <= temperatures[i])
            {
                st.pop();
            }
            if (!st.empty()) 
            {
                ans[i] = st.top() - i;
            }
            st.push(i);
        }
        return ans;
    }
};



## 5.Min stack-
**Link:** https://leetcode.com/problems/min-stack/description/

class MinStack 
{
    vector<int>v;
public:
    MinStack() 
    {
       
    }
    void push(int val) 
    {
      v.push_back(val);
    }
    void pop() 
    {
       v.pop_back();
    }
    int top() 
    {
       int top_ele=v.back();
        return top_ele;
    }
    int getMin() 
    {
        int min_ele=*min_element(v.begin(),v.end());
        return min_ele;
    }
};



