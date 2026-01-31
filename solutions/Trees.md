# Trees-
This file contains all the solutions of the trees questions of algomap leetcode sheet.
Language used-C++

## 1.Invert binary tree-
**Link:** https://leetcode.com/problems/invert-binary-tree/description/

class Solution 
{
public:
    TreeNode* invertTree(TreeNode* root) 
    {
        if(root==NULL)
        return root;
        TreeNode* temp=root->left;
        root->left=root->right;
        root->right=temp;
        invertTree(root->left);
        invertTree(root->right);
        return root;
    }
};


## 2.Maximum depth of binary tree-
**Link:** https://leetcode.com/problems/maximum-depth-of-binary-tree/description/

class Solution 
{
public:
    int maxDepth(TreeNode* root)
    {
        if(root==NULL)
        return 0;
        int ld=maxDepth(root->left);
        int rd=maxDepth(root->right);
        return max(ld,rd)+1;
    }
};



## 3.Balanced binary tree-
**Link:** https://leetcode.com/problems/balanced-binary-tree/description/

class Solution 
{
public:
int height(TreeNode* root)
{
if(root==NULL)
return 0;
int lh=height(root->left);
if(lh==-1)
return -1;
int rh=height(root->right);
if(rh==-1)
return -1;
if(abs(lh-rh)>1)
return -1;
return max(lh,rh)+1;
}
    bool isBalanced(TreeNode* root) 
    {
        return height(root)!=-1;
    }
};



## 4.Diameter of binary tree-
**Link:** https://leetcode.com/problems/diameter-of-binary-tree/description/

class Solution 
{
public:
pair<int,int>heightDiameter(TreeNode* root)
{
    if(root==NULL)
    {
        pair<int,int>p;
        p.first=0;
        p.second=0;
        return p;
    }
    pair<int,int>left=heightDiameter(root->left);
    pair<int,int>right=heightDiameter(root->right);
    int lh=left.first;
    int ld=left.second;
    int rh=right.first;
    int rd=right.second;
    int height=max(lh,rh)+1;
    int diameter=max(lh+rh,max(ld,rd));
    pair<int,int>p;
    p.first=height;
    p.second=diameter;
    return p;
}
    int diameterOfBinaryTree(TreeNode* root) 
    {
        pair<int,int>p=heightDiameter(root);
        return p.second;
    }
};



## 5.Same binary tree-
**Link:** https://leetcode.com/problems/same-tree/description/

class Solution 
{
public:
    bool isSameTree(TreeNode* p, TreeNode* q) 
    {
        if (p == NULL && q == NULL) return true;
        if (p == NULL || q == NULL) return false;
        if (p->val != q->val) return false;
        return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
};



## 6.Symmetric tree-
**Link:** https://leetcode.com/problems/symmetric-tree/description/

class Solution 
{
public:
bool helper(TreeNode* left1,TreeNode* right1)
{
    if(left1==NULL && right1!=NULL)
    return false;
    if(left1!=NULL && right1==NULL)
    return false;
    if(left1==NULL && right1==NULL)
    return true;
    if(left1->val!=right1->val)
    return false;
    return helper(left1->left,right1->right) && helper(left1->right,right1->left);
}
    bool isSymmetric(TreeNode* root) 
    {
       if(root==NULL)
       return true;
       return helper(root->left,root->right);
    }
};



## 7.Path sum-
**Link:** https://leetcode.com/problems/path-sum/description/

class Solution 
{
public:
    bool hasPathSum(TreeNode* root, int targetSum) 
    {
        if(root==NULL)
        return false;
        if(root->left==NULL && root->right==NULL)
        return targetSum==root->val;
        int rem=targetSum-root->val;
        return hasPathSum(root->left,rem)||hasPathSum(root->right,rem);
    }
};



## 8.Subtree of another tree-
**Link:** https://leetcode.com/problems/subtree-of-another-tree/description/

class Solution 
{
public:
    bool isSame(TreeNode* root, TreeNode* subRoot) 
    {
        if(root == NULL && subRoot == NULL) return true;
        if(root == NULL || subRoot == NULL) return false;
        if(root->val != subRoot->val) return false;
        return isSame(root->left, subRoot->left) && isSame(root->right, subRoot->right);
    }
    bool isSubtree(TreeNode* root, TreeNode* subRoot) 
    {
        if(root == NULL) return false;
        if(isSame(root, subRoot)) return true;
        return isSubtree(root->left, subRoot) || isSubtree(root->right, subRoot);
    }
};



## 9.Binary tree level order traversal-
**Link:** https://leetcode.com/problems/binary-tree-level-order-traversal/description/

class Solution 
{
public:
    vector<vector<int>> levelOrder(TreeNode* root) 
    {
        vector<vector<int>>ans;
        vector<int>temp;
        if(root==NULL)
        return ans;
        queue<TreeNode*>q;
        q.push(root);
        q.push(NULL);
        while(!q.empty())
        {
            TreeNode* f=q.front();
            q.pop();
            if(f==NULL)
            {
                ans.push_back(temp);
                temp.clear();
                if(!q.empty())
                {
                    q.push(NULL);
                }
            }
                else
                {
                    temp.push_back(f->val);
                    if(f->left)
                    {
                        q.push(f->left);
                    }
                    if(f->right)
                    {
                        q.push(f->right);
                    }
                }
        }
return ans;
    }
};



## 10.Kth smallest element in a bst-
**Link:** https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/

class Solution 
{
public:
void inorder(TreeNode* root,int k,vector<int>&ans)
{
        if(root==NULL)
        return;
        inorder(root->left,k,ans);
        ans.push_back(root->val);
        inorder(root->right,k,ans);
}
    int kthSmallest(TreeNode* root, int k) 
    {
        vector<int>ans;
        inorder(root,k,ans);
        return ans[k-1];
    }
};



## 11.Minimum absolute difference in bst-
**Link:** https://leetcode.com/problems/minimum-absolute-difference-in-bst/description/

class Solution 
{
public:
    int prevVal = -1;
    int minDiff = INT_MAX;
    void inorder(TreeNode* root) 
    {
        if (root==NULL) 
        return;
        inorder(root->left);
        if (prevVal != -1) 
        {
            minDiff = min(minDiff, root->val - prevVal);
        }
        prevVal = root->val;
        inorder(root->right);
    }
    int getMinimumDifference(TreeNode* root) 
    {
        inorder(root);
        return minDiff;
    }
};



## 12.Valid binary search tree-
**Link:** https://leetcode.com/problems/validate-binary-search-tree/description/

class Solution 
{
public:
int prev=-2;
bool ans=true;
void inorder(TreeNode* root)
{
if(root==NULL)
return;
inorder(root->left);
if(prev!=-2)
{
    if(root->val<=prev)
    {
    ans=false;
    return;
    }
}
prev=root->val;
inorder(root->right); 
}
    bool isValidBST(TreeNode* root) 
    {
        inorder(root);
        return ans;
    }
};



## 13.Lowest common ancestor of a binary search tree-
**Link:** https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/

class Solution 
{
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) 
    {
    TreeNode* lca=root;
    while(root!=NULL)
    {
    if(root->val<p->val && root->val<q->val)
    root=root->right;
    else if(root->val>p->val && root->val>q->val)
    root=root->left;
    else
    {
        lca=root;
        break;
    }
    }
        return lca;
    }
};


