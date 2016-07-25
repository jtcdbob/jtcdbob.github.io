---
title:  "Leetcode Revisted"
excerpt: "Notes for working on Revisiting leetcode"
categories:
  - Blog
tags:
  - CODE_DEBUG_LIFE
use_math: false
---

##### 344.Reverse String

Call library function.

```cpp
string reverseString(string s) {
    reverse(s.begin(), s.end());
    return s;
}
```

##### 292.Nim Game

Whoever gets 4 for the other part will win.

```cpp
bool canWinNim(int n) {
    return n%4;
}
```

##### 371. Sum of Two Integers

Use bit operation. This is a smart way to do it. (Whatever.)

```cpp
int getSum(int a, int b) {
    while (b != 0) {
        int c = a;
        a = a ^ b;
        b = c & b;
        b <<= 1;
    }
    return a;
}
```

##### 258. Add Digits

Find a pattern that loops from 1 to 9.

```cpp
int addDigits(int num) {
    if (!num) return 0;
    else return num%9 ? num%9 : 9;
}
```

##### 104. Maximum Depth of Binary Tree

Use recursion to get the maximum depth (DFS will do just fine).

```cpp
int maxDepth(TreeNode* root) {
    if (root == NULL) return 0;
    return max(maxDepth(root->left), maxDepth(root->right)) + 1;
}
```

##### 226. Invert Binary Tree

Recursion, swap with a tmp variable, DFS.

```cpp
TreeNode* invertTree(TreeNode* root) {
    if (root != NULL) {
        TreeNode* tmpNode = root->left;
        root->left = root->right;
        root->right = tmpNode;
        invertTree(root->left);
        invertTree(root->right);
    }
    return root;
}
```

##### 283. Move Zeroes

Use a counter to keep track of the non-zero elements in the array and replace them in place.

```cpp
void moveZeroes(vector<int>& nums) {
    int n = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i]) {
            nums[n++] = nums[i];
        }
    }
    for (int j = n; j < nums.size(); j++) {
        nums[j] = 0;
    }
}
```

##### 349. Intersection of Two Arrays

Use a hash table to keep track of nums in nums1 and compare it with nums2.

```cpp
vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
    unordered_set<int> dictForNums1;
    vector<int> intersectVectorSet;
    for (int num : nums1) {
        dictForNums1.insert(num);
    }
    for (int num : nums2) {
        if (dictForNums1.find(num) != dictForNums1.end()) {
            intersectVectorSet.push_back(num);
            dictForNums1.erase(num);
        }
    }
    return intersectVectorSet;
}
```

##### 237. Delete Node in a Linked List

Replace the current value with the next value and link it to next next one. Consider edge cases.

```cpp
void deleteNode(ListNode* node) {
    if (node) {
        if (!node->next) {
            node = NULL;
        } else {
            node->val = node->next->val;
            node->next = node->next->next;
        }
    }
}
```

##### 100. Same Tree

Compare node value, then recursively compare left and right nodes.

```cpp
bool isSameTree(TreeNode* p, TreeNode* q) {
    if ((p!=NULL) ^ (q!=NULL)) return false;
    if ((p!=NULL) & (q!=NULL)) {
        if (p->val != q->val) return false;
        return isSameTree(p->left, q->left) & isSameTree(p->right, q->right);
    }
    return true;
}
```
