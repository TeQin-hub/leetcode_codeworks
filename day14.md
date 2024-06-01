# 二叉树

## 递归遍历

```c++
struct TreeNode{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(): val(0),left(NULL),right(NULL) {}
    TreeeNode(int x): val(x),left(NULL),right(NULL) {}
    TreeNode(int x, TreeNode* Lp,TreeNode* Rp):val(x),left(Lp),right(Rp) {}
}

void traversal(TreeNode *node, vector<int>& vec){
    if(node == NULL) return;
    vec.push_back(node->val);
    traversal(node->left,vec);
    traversal(node->right,vec);
}
vector<int> preOrderTraversal(TreeNode *root){
    vector<int> result;
    traversal(root,result);
    return result;
}
```

练习

```c++
struct TreeNode{
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode():val(),left(NULL),right(NULL) {}
    TreeNode(int x):val(x),left(NULL),right(NULL) {}
    TreeNode(int x, TreeNode* lp, TreeNode* rp):val(x), left(lp). right(rp) {}
};
void traversal(TreeNode* node, vector<int> vec){
    if(node == NULL) return;
    vec.push_back(node->val);
    traversal(node->left,vec);
    traversal(node->right,vec);
}
vector<int> preOrderTraversal(TreeNode* root){
    vector<int> result;
    traversal(root, result);
    return result;
}
```



## 迭代遍历

### 前序遍历

中左右

```c++
vector<int> preOrderTraversal(TreeNode* root){
    vector<int> result;
    stack<TreeNode*> st;
    if(root == Null) return result;
    st.push(root);
    while(!st.empty()){
        TreeNode* node = st.top();
        st.pop();
        result.push_back(node->val);
        if(node->right) st.push(node->right);
        if(node->left) st.push(node->left);
    }
    return result;
}
```

练习

```c++
vector<int> preOrderTraversal(TreeNode* root){
    vector<int> result;
    stack<TreeNode*> st;
    if(root == NULL) return result;
    st.push(root);
    while(!st.empty()){
        TreeNode* node = st.top();
        st.pop();
        result.push_back(node->val);
        if(node->right) st.push(node->right);
        if(node->left) st.push(node->left);
    }
    return result;
}
```



### 后序遍历

先中右左，在reverse后变为左右中

```c++
vector<int> postOrderTraversal(TreeNode* root){
    vector<int> result;
    stack<TreeNode*> st;
    if(root == NULL) return result;
    st.push(root);
    while(!st.empty()){
        TreeNode* node = st.top();
        st.pop();
        result.push_back(node->val);
        if(node->left) st.push(node->left);
        if(node->right) st.push(node->right);
    }
    reverse(result.begin(),result.end());
    return result;
}
```

练习

```c++
vector<int> postOrderTraversal(TreeNode* root){
    vector<int> result;
    stack<TreeNode*> st;
    if(root == NULL) return result;
    st.push(root);
    while(!st.empty()){
        TreeNode* node = st.top();
        st.pop();
        result.push_back(node->val);
        if(node->left) st.push(node->left);
        if(node->right) st.push(node->right);
    }
    reverse(result.begin(),result.end());
    return result;
}
```



### 中序遍历

```c++
vector<int> inOrderTraversal(TreeNode* root){
    vector<int> result;
    stack<TreeNode*> st;
    TreeNode *cur = root;
    while(cur != NULL || !st.empty()){
        if(cur){
            st.push(cur->left);
            cur = cur->left;
        }else{
            cur = st.top();
            st.pop();
            result.push_back(cur->val);
            cur = cur->right;
        }
    }
    return result;
}
```

练习

```c++
vector<int> inOrderTraversal(TreeNode* root){
    vector<int> result;
    stack<TreeNode*> st;
    TreeNode* cur = root;
    while(cur || !st.empty()){
        if(cur){
            st.push(cur->left);
            cur = cur->left;
        }else{
            cur = st.top();
            st.pop();
            result.push_back(cur->val);
            cur = cur->right;
        }
    }
    return result;
}
```

