# [Leetcode 297. 二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)

## Problem description:

> 序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。
>
> 请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。
>

## Example:

```
你可以将以下二叉树：

    1
   / \
  2   3
     / \
    4   5

序列化为 "[1,2,3,null,null,4,5]"

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```

**提示:** 这与 LeetCode 目前使用的方式一致，详情请参阅 LeetCode 序列化二叉树的格式。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。

**说明:** 不要使用类的成员 / 全局 / 静态变量来存储状态，你的序列化和反序列化算法应该是无状态的。

## Solution:

### Tags:

### *[Data structure](https://github.com/yang-233/Algorithm-note/tree/master/Data-structure)* 

### How to do:

> 注意题意，测评方法是给一棵二叉树，先让你序列化再反序列化，看看得到的二叉树是否雨原来相同，因此不需要按照官方所给的方法来做。实际上，指要将空指针也打印出来，先序遍历就可以解决问题了，并且更简洁。

### Code:

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */

class Codec {
public:

    string to_str(int val) {
        string s = "";
        while (val) {
            s += val % 10 + '0';
            val /= 10;
        }
        reverse(s.begin(), s.end());
        if(s == "")
            s = "0";
        return s;
    }

    int to_int(const string &s) {
        int val = 0;
        for (auto i : s)
            val = val * 10 + i - '0';
        return val;
    }
    // static vector<string> split(const string& s, const string& delimiters = " ")// 这个只能使用单字符为，传入多字符时指每个字符都为分隔符
    // {
    //     vector<string> tokens;
    //     string::size_type lastPos = s.find_first_not_of(delimiters, 0);
    //     string::size_type pos = s.find_first_of(delimiters, lastPos);
    //     while (string::npos != pos || string::npos != lastPos) {
    //         tokens.push_back(s.substr(lastPos, pos - lastPos));
    //         lastPos = s.find_first_not_of(delimiters, pos);
    //         pos = s.find_first_of(delimiters, lastPos);
    //     }
    //     return tokens;
    // }

    static vector<string> split(const string & s) {
        vector<string> res;
        if(s.empty())
            return res;
        int start = 0;
        for(int i = 0; i < s.size(); ++i) {
            if(s[i] == ',') {
                if(i > start)
                    res.push_back(s.substr(start, i - start));
                    start = i + 1;
            } 
        }
        if(start < s.size())
            res.push_back(s.substr(start, s.size() - start));
        return res;
    }
    //vector<string> split(const string& s, const string& sep) { // 分割字符串
    //    
    //    char* token = strtok(s.data(), sep.c_str());

    //    int len = sep.size(), offset = 0;
    //    vector<string> res;
    //    for (int pos = 0;; offset = pos + len) {
    //        pos = s.find(sep, offset);//搜索分隔符
    //        if (pos == s.npos)//找不到了
    //            break;
    //        else {
    //            if(pos > offset)//如果当前也是分隔符，则不添加
    //                res.push_back(s.substr(offset, pos - offset));
    //        }
    //    }
    //    if (offset < s.size()) // 到结尾的字符串
    //        res.push_back(s.substr(offset, s.size() - offset));
    //    return res;
    //}

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        if(root == nullptr)
            return "[]";
        queue<TreeNode*> que;
        vector<string> vec;
        string res = "[";
        que.push(root);
        while(!que.empty()) {
            TreeNode* t = que.front();
            que.pop();
            if(t == nullptr)
                vec.push_back("null");
            else {
                vec.push_back(to_str(t->val));
                que.push(t->left);
                que.push(t->right);
            }
        }
        int last = vec.size() - 1;
        while (vec[last] == "null")
            --last;
        for(int i = 0; i < last; ++i)
            res += vec[i] + ",";
        res += vec[last] + "]";
        return res;
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        if(data == "[]")
            return nullptr;
        queue<TreeNode**> que;
        TreeNode* t;
        TreeNode** root = &t;//临时用一个指针记录根节点
        que.push(root);
        for(auto i : split(data.substr(1, data.size() - 2))) {//如果为"[]"这里会报错
            auto node = que.front();
            que.pop();
            if(i == "null") //当前节点为空指针
                *node = nullptr;
            else {
                *node = new TreeNode(to_int(i));//为当前节点赋值
                que.push(&((*node)->left));//把新建节点的左儿子节点的地址保存起来
                que.push(&((*node)->right));
            }
        }
        return *root;
    }
    
    void check(TreeNode *root) {
        if (root == nullptr) {
            return;
        }
        check(root->left);
        cout << root->val << endl;
        check(root->right);
    }
};

// Your Codec object will be instantiated and called as such:
// Codec codec;
// codec.deserialize(codec.serialize(root));
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(n)*

