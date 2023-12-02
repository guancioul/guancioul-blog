---
title: "[Algorithm]Level Order Traversal(廣度優先走訪)"
toc: true
categories: 
    - Algorithm
tags: 
    - Algorithm
    - Leetcode
published: false
---

樹狀結構一層一層讀取的方法

![image-center]({{site.url}}{{site.baseurl}}/assets/images/Algorithm/Level-Order-Traversal.png){: .align-center}

## Solution
1. 先建立一個Queue，Queue中的資料結構為TreeNode，`queue<TreeNode>`，並且將Tree中的root push到Queue中<br>
    ```c++
    void levelOrder(TreeNode * root){
        queue<TreeNode*> q;
        if(!root) return;
        q.push(root); // Queue [TreeNode(3)]
    }
    ```
2. 設定一個while loop，如果Queue是空的，就跳出while迴圈
    ```c++
    void levelOrder(TreeNode * root){
        queue<TreeNode*> q;
        if(!root) return;
        q.push(root); // Queue [TreeNode(3)]
        while(!q.empty()){
        }
    }
    ```
3. while loop中再設定一個for loop，這個for要跑的次數取決於Queue的size，這個時候n=1，會將level 0的值讀出來
    ```c++
    void levelOrder(TreeNode * root){
        queue<TreeNode*> q;
        if(!root) return;
        q.push(root); // Queue [TreeNode(3)]
        while(!q.empty()){
            int n = q.size(); // n=1
            for(int i=0; i<n; i++){
            }
        }
    }
    ```
4. 這個時候我們會先用一個TreeNode將Queue的第一個值用變數curr存起來，並且將Queue中的第一個值pop掉，這個curr就是我們目前走訪到的位置，可以把這個值印出來
    ```c++
    void levelOrder(TreeNode * root){
        queue<TreeNode*> q;
        if(!root) return;
        q.push(root); // Queue [TreeNode(3)]
        while(!q.empty()){
            int n = q.size(); // n=1
            for(int i=0; i<n; i++){
                TreeNode* curr = q.front(); // curr = TreeNode(3)
                q.pop(); // Queue []
                cout << curr->val << "\n"; // 3
            }
        }
    }
    ```
5. 再來會去尋找curr的left跟right有沒有值，如果有的話一樣push到Queue中
    ```c++
    void levelOrder(TreeNode * root){
        queue<TreeNode*> q;
        if(!root) return;
        q.push(root); // Queue [TreeNode(3)]
        while(!q.empty()){
            int n = q.size(); // n=1
            for(int i=0; i<n; i++){
                TreeNode* curr = q.front(); // curr = TreeNode(3)
                q.pop(); // Queue []
                cout << curr->val << "\n"; // 3 
                if(curr->left) q.push(curr->left); // Queue [TreeNode(2)]
                if(curr->right) q.push(curr->right); // Queue [TreeNode(2), TreeNode(5)]
            }
        }
    }
    ```
6. 由於一開始只有root一個值，所以第一次迴圈的時候n=1，只會執行一次for loop，再來會回到`int n = q.size()`這個地方，由於Queue裡面有兩個值，所以現在n=2，會把level 1的地方讀出來。這邊執行的是跑完TreeNode(2)的結果
    ```c++
    void levelOrder(TreeNode * root){
        queue<TreeNode*> q;
        if(!root) return;
        q.push(root); // Queue [TreeNode(3)]
        while(!q.empty()){
            int n = q.size(); // n=2
            for(int i=0; i<n; i++){
                TreeNode* curr = q.front(); // curr = TreeNode(2)
                q.pop(); // Queue [TreeNode(5)]
                cout << curr->val << "\n"; // 3, 2
                if(curr->left) q.push(curr->left); // Queue [TreeNode(5), TreeNode(1)]
                if(curr->right) q.push(curr->right); // Queue [TreeNode(5), TreeNode(1)]
            }
        }
    }
    ```
7. 再來執行跑TreeNode(5)的結果
    ```c++
    void levelOrder(TreeNode * root){
        queue<TreeNode*> q;
        if(!root) return;
        q.push(root); // Queue [TreeNode(3)]
        while(!q.empty()){
            int n = q.size(); // n=2
            for(int i=0; i<n; i++){
                TreeNode* curr = q.front(); // curr = TreeNode(5)
                q.pop(); // Queue [TreeNode(1)]
                cout << curr->val << "\n"; // 3, 2, 5
                if(curr->left) q.push(curr->left); // Queue [TreeNode(1), TreeNode(4)]
                if(curr->right) q.push(curr->right); // Queue [TreeNode(1), TreeNode(4), TreeNode(7)]
            }
        }
    }
    ```
8. 這個時候跑完level 1，跳出for loop後，接著跑level 2的值，TreeNode(1)
    ```c++
    void levelOrder(TreeNode * root){
        queue<TreeNode*> q;
        if(!root) return;
        q.push(root); // Queue [TreeNode(3)]
        while(!q.empty()){
            int n = q.size(); // n=3
            for(int i=0; i<n; i++){
                TreeNode* curr = q.front(); // curr = TreeNode(1)
                q.pop(); // Queue [TreeNode(4), TreeNode(7)]
                cout << curr->val << "\n"; // 3, 2, 5, 1
                if(curr->left) q.push(curr->left); // Queue [TreeNode(4), TreeNode(7)]
                if(curr->right) q.push(curr->right); // Queue [TreeNode(4), TreeNode(7)]
            }
        }
    }
    ```
9. level 2，TreeNode(4)
    ```c++
    void levelOrder(TreeNode * root){
        queue<TreeNode*> q;
        if(!root) return;
        q.push(root); // Queue [TreeNode(3)]
        while(!q.empty()){
            int n = q.size(); // n=3
            for(int i=0; i<n; i++){
                TreeNode* curr = q.front(); // curr = TreeNode(4)
                q.pop(); // Queue [TreeNode(7)]
                cout << curr->val << "\n"; // 3, 2, 5, 1, 4
                if(curr->left) q.push(curr->left); // Queue [TreeNode(7)]
                if(curr->right) q.push(curr->right); // Queue [TreeNode(7)]
            }
        }
    }
    ```
10. level 2，TreeNode(7)
    ```c++
    void levelOrder(TreeNode * root){
        queue<TreeNode*> q;
        if(!root) return;
        q.push(root); // Queue [TreeNode(3)]
        while(!q.empty()){
            int n = q.size(); // n=3
            for(int i=0; i<n; i++){
                TreeNode* curr = q.front(); // curr = TreeNode(7)
                q.pop(); // Queue []
                cout << curr->val << "\n"; // 3, 2, 5, 1, 4, 7
                if(curr->left) q.push(curr->left); // Queue []
                if(curr->right) q.push(curr->right); // Queue []
            }
        }
    }
    ```
11. 目前Queue已經空了，所以會跳出while迴圈，程式也就結束了，這邊可以看到印出的結果是
    ```
    3, 2, 5, 1, 4, 7
    ```
    剛好對應一層一層讀取的值

## Code
    ```c++
    void levelOrder(TreeNode * root){
        queue<TreeNode*> q;
        if(!root) return;
        q.push(root); 
        while(!q.empty()){
            int n = q.size();
            for(int i=0; i<n; i++){
                TreeNode* curr = q.front();
                q.pop();
                cout << curr->val << "\n";
                if(curr->left) q.push(curr->left);
                if(curr->right) q.push(curr->right);
            }
        }
    }
    ```

## 參考資料
* [Binary Tree Level Order Traversal - Drawing The Parallel Between Trees & Graphs](https://www.youtube.com/watch?v=gcR28Hc2TNQ&ab_channel=BackToBackSWE)