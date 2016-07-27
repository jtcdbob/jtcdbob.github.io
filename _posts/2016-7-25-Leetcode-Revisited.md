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

##### 171. Excel Sheet Column Number
Easy number conversion. Base = 26.

```cpp
int titleToNumber(string s) {
    int sum = 0;
    int N = s.size() - 1;
    for (int i = N; i > -1; i--) {
        sum += (s[i] - 'A' + 1) * pow(26, N-i);
    }
    return sum;
}
```

##### 242. Valid Anagram
Use an array of 26 to count the occurance of letters in each word.

```cpp
bool isAnagram(string s, string t) {
    if (s.size() - t.size()) return false;
    vector<int> myDict(26, 0);
    for (int i = 0; i < s.size(); i++) {
        myDict[s[i]-'a']++;
        myDict[t[i]-'a']--;
    }
    for (int num : myDict) {
        if (num) return false;
    }
    return true;
}
```

##### 169. Majority Element
Use voting algorithm to find the popular element.

```cpp
int majorityElement(vector<int>& nums) {
    if (nums.empty()) return -1;
    int popularElement = nums.front();
    int counter = 1;
    for (int i = 1; i < nums.size(); i++) {
        if (nums[i] == popularElement) {
            counter++;
        }
        else {
            if (--counter < 0) {
                popularElement = nums[i];
                counter = 1;
            }
        }
    }
    return popularElement;
}
```

##### 217. Contains Duplicate
Use a hashtable to keep track of existing numbers. (Or simply sort the array and count, which seems as fast if not faster.)

```cpp
bool containsDuplicate(vector<int>& nums) {
    unordered_set<int> existedNums;
    for (int num : nums) {
        if(existedNums.find(num) != existedNums.end()) return true;
        else existedNums.insert(num);
    }
    return false;
}
```

##### 350. Intersection of Two Arrays II
Use a map to keep track of the number of each element in nums1 and iterate through nums2 to get the intersected occurance.

```cpp
vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
    unordered_map<int, int> myMap;
    vector<int> intersection;
    for (int num : nums1) {
        if(myMap.find(num) != myMap.end()) myMap[num]++;
        else myMap[num] = 1;
    }
    for (int num : nums2) {
        if((myMap.find(num) != myMap.end()) && myMap[num]) {
            intersection.push_back(num);
            myMap[num]--;
        }
    }
    return intersection;
}
```

##### 206. Reverse Linked List
Basic linked list operations. Use a tmp to store intermediate values.

```cpp
ListNode* reverseList(ListNode* head) {
    if (head == NULL || head->next == NULL) return head;
    ListNode* last = NULL;
    while (head->next != NULL) {
        ListNode* tmp = head->next;
        head->next = last;
        last = head;
        head = tmp;
    }
    head->next = last;
    return head;
}
```

##### 326. Power of Three
Stupid.

```cpp
bool isPowerOfThree(int n) {
    if(!n) return false;
    double log3 = log10(n)/log10(3);
    return log3 == floor(log3);
}
```

##### 231. Power of Two
Stupid++;

```cpp
bool isPowerOfTwo(int n) {
    if(!n) return false;
    return log2(n) == floor(log2(n));
}
```

##### 191. Number of 1 Bits
Move to the right and count the number of 1's at the rightmost.

```cpp
int hammingWeight(uint32_t n) {
    int counter = 0;
    while(n) {
        counter += n%2;
        n >>= 1;
    }
    return counter;
}
```

##### 263. Ugly Number
Exhause the factor and see if it ends up to be 1.

```cpp
bool isUgly(int num) {
    if (num < 1) return false;
    while (!(num % 2)) num /= 2;
    while (!(num % 3)) num /= 3;
    while (!(num % 5)) num /= 5;
    return (num == 1);
}
```

##### 235. Lowest Common Ancestor of a Binary Search Tree
Use dfs to find the target nodes in each branch. When there are two nodes found from the branches in one root, return the root.

```cpp
class Solution {
public:
    TreeNode* lca = NULL;

    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        dfs(root, p, q);
        return lca;
    }

    int dfs(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == NULL) return 0;
        int left = dfs(root->left, p, q);
        int right = dfs(root->right, p, q);
        if(left < 0 || right < 0) return -1;
        int nodeFount = 0;
        if (root->val == p->val) nodeFount += 1;
        if (root->val == q->val) nodeFount += 1;
        nodeFount += left + right;
        if (nodeFount == 2) {
            lca = root;
            nodeFount = -1;
        }
        return nodeFount;
    }
};
```

##### 83. Remove Duplicates from Sorted List
When a duplicate is encountered, just skip it and link to the next one.

```cpp
ListNode* deleteDuplicates(ListNode* head) {
    ListNode* tail = head;
    while(tail != NULL) {
        while(tail->next != NULL && tail->val == tail->next->val) {
            tail->next = tail->next->next;
        }
        tail = tail->next;
    }
    return head;
}
```

##### 70. Climbing Stairs
Dynamic programming. Do NOT use recursion because the time complexity is huge.

```cpp
int climbStairs(int n) {
    if(n < 1) return 0;
    if(n == 1) return 1;
    if(n == 2) return 2;
    vector<int> series(n, 0);
    series[0] = 1;
    series[1] = 2;
    for(int i = 2; i < n; i++){
        series[i] = series[i-1] + series[i-2];
    }
    return series.back();
}
```
