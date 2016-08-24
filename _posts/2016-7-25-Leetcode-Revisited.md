---
title:  "Leetcode Revisted"
excerpt: "Notes for working on Revisiting leetcode"
categories:
  - Blog
tags:
  - CODE_DEBUG_LIFE
use_math: false
---

## Easy

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

##### 299. Bulls and Cows
Compare two strings character by character. If the characters matches add it to bulls. If the characters don't match, add it to two maps. When the comparison is done, check the two maps to count the number of cows.

```cpp
string getHint(string secret, string guess) {
   int bull = 0, cow = 0;
   int secretLetterCount[10] = {0};
   int guessLetterCount[10] = {0};
   // Assuming the sizes for secret and guess are the same.
   int N = secret.size();
   for(int i = 0; i < N; i++) {
       if (secret[i] == guess[i]) {
           bull++;
       } else {
           secretLetterCount[secret[i]-'0']++;
           guessLetterCount[guess[i]-'0']++;
       }
   }
   for(int i = 0; i < 10; i++) {
       cow += min(secretLetterCount[i], guessLetterCount[i]);
   }
   return to_string(bull) + "A" + to_string(cow) + "B";
}
```

##### 101. Symmetric Tree
Use dfs to compare two branches of the tree. If each node is symmetric to its counterpart, the tree is symmetric.

```cpp
bool isSymmetric(TreeNode* root) {
    if (root == NULL) return true;
    return dfsCmp(root->left, root->right);
}
bool dfsCmp(TreeNode* leftNode, TreeNode* rightNode) {
    if (leftNode == NULL && rightNode == NULL) return true;
    if (leftNode == NULL ^ rightNode == NULL) return false;
    if (leftNode->val != rightNode->val) return false;
    return dfsCmp(leftNode->left, rightNode->right) && dfsCmp(leftNode->right, rightNode->left);
}
```

##### 27. Remove Element
Use a counter to keep track of distinct elements and replace the element in place till the end.

```cpp
int removeElement(vector<int>& nums, int val) {
    int counter = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] != val) nums[counter++] = nums[i];
    }
    return counter;
}
```

##### 198. House Robber
Use dynamic programming to get the maximum possible outcome.

```cpp
int rob(vector<int>& nums) {
    if (nums.empty()) return 0;
    else if (nums.size() > 1) nums[1] = max(nums[0], nums[1]);
    for (int i = 2; i < nums.size(); i++){
        nums[i] = max(nums[i] + nums[i-2], nums[i-1]);
    }
    return nums.back();
}
```

##### 141. Linked List Cycle
Use a fast and a slow node to travel through the list. If there is a cycle, the fast and slow nodes will eventually converge.

```cpp
bool hasCycle(ListNode *head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (slow != NULL && fast != NULL) {
        slow = slow->next;
        if(fast->next != NULL) {
            fast = fast->next->next;
        } else return false;
        if(slow == fast) return true;
    }
    return false;
}
```

##### 342. Power of Four
Well, just do log, I don't care.

```cpp
bool isPowerOfFour(int num) {
    if (num == 5 || num < 1) return false;
    double ans = log(num) / log(4);
    return round(ans) == ans;
}
```

##### 24. Swap Nodes in Pairs
Nothing much, just swap the pair and move two steps forward a time.

```cpp
ListNode* swapPairs(ListNode* head) {
    ListNode* tail = head;
    while (tail != NULL && tail->next != NULL) {
        int tmp = tail->val;
        tail->val = tail->next->val;
        tail->next->val = tmp;
        tail = tail->next->next;
    }
    return head;
}
```

##### 345. Reverse Vowels of a String
Converge from both left and right side of the string. Stop when a vowel is encountered, then swap the two in place.

```cpp
class Solution {
public:
    const unordered_set<char> VOWELS = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};

    string reverseVowels(string s) {
        int l = 0;
        int r = s.size() - 1;
        while (l < r) {
            while (VOWELS.find(s[l]) == VOWELS.end()) l++;
            while (VOWELS.find(s[r]) == VOWELS.end()) r--;
            if (l < r) {
                char tmp = s[l];
                s[l++] = s[r];
                s[r--] = tmp;
            }
        }
        return s;
    }
};
```

##### 121. Best Time to Buy and Sell Stock
Just get the maximum difference between minimum and maximum after it.

```cpp
int maxProfit(vector<int>& prices) {
    if (prices.empty()) return 0;
    int tmpMax = 0;
    int tmpMin = INT_MAX;
    int tmpMaxDiff = 0;
    for (int price : prices) {
        if (price < tmpMin) {
            tmpMaxDiff = max(tmpMaxDiff, tmpMax - tmpMin);
            tmpMin = price;
            tmpMax = tmpMin;
        } else if (price > tmpMax) {
            tmpMax = price;
        }
    }
    return max(tmpMaxDiff, tmpMax - tmpMin);
}
```

##### 383. Ransom Note
Use two maps to keep track of the number of letters in both string. If there are enough letters, return true.

```cpp
bool canConstruct(string ransomNote, string magazine) {
    int counter[26] = {0};
    for (char letter : magazine) {
        counter[letter - 'a']++;
    }
    for (char letter : ransomNote) {
        if (--counter[letter - 'a'] < 0) return false;
    }
    return true;
}
```

##### 374. Guess Number Higher or Lower
Basically a binary search.

```cpp
int guessNumber(int n) {
    int myLowGuess = 1;
    int myHighGuess = n;

    int myGuess = (int) (myHighGuess - myLowGuess) / 2 + myLowGuess;
    int result = guess(myGuess);
    while(result && (myHighGuess > (myLowGuess + 1))) {
        if (result < 0) {
            myHighGuess = myGuess;
        } else {
            myLowGuess = myGuess;
        }
        myGuess = (int) (myHighGuess - myLowGuess) / 2 + myLowGuess;
        cout << myHighGuess << "\t" << myLowGuess << "\t" << myGuess << endl;
        result = guess(myGuess);
    }
    if (guess(myGuess) != 0) return guess(myGuess) > 0 ? myHighGuess : myLowGuess;
    else return myGuess;
}
```

##### 112. Path Sum
Do a dfs search for the path sum.

```cpp
bool hasPathSum(TreeNode* root, int sum) {
    int pathSum = 0;
    if(root == NULL) return false;
    return dfs(root, sum, pathSum);
}

bool dfs(TreeNode* node, const int target, int pathSum) {
    pathSum += node->val;
    if(node->left == NULL && node->right == NULL) return target == pathSum;
    bool leftRes = false, rightRes = false;
    if (node->left != NULL) leftRes = dfs(node->left, target, pathSum);
    if (node->right != NULL) rightRes = dfs(node->right, target, pathSum);
    return leftRes || rightRes;
}
```

##### 107. Binary Tree Level Order Traversal II
Nothing much, just plain bfs traversal. Make sure to keep track of the elements in each level. This can be done by using two queues.

```cpp
vector<vector<int>> levelOrderBottom(TreeNode* root) {
    vector<vector<int>> results;
    vector<int> rowResults;
    queue<TreeNode*> bfsQueue;
    queue<TreeNode*> tmpQueue;
    if(root != NULL) bfsQueue.push(root);
    while (!bfsQueue.empty()) {
        TreeNode* tmpNode = bfsQueue.front();
        bfsQueue.pop();
        rowResults.push_back(tmpNode->val);
        if(tmpNode->left != NULL) tmpQueue.push(tmpNode->left);
        if(tmpNode->right != NULL) tmpQueue.push(tmpNode->right);
        if (bfsQueue.empty() && !tmpQueue.empty()) {
            swap(bfsQueue, tmpQueue);
            results.push_back(rowResults);
            rowResults.clear();
        }
    }
    if(!rowResults.empty()) results.push_back(rowResults);
    reverse(results.begin(), results.end());
    return results;
}
```

##### 118. Pascal's Triangle
For each row, add a `1` to its last row and then combine two elements (sort of dp).

```cpp
vector<vector<int>> generate(int numRows) {
    if(numRows < 1) return vector<vector<int>>{};
    vector<vector<int>> results = {vector<int> {1}};
    for(int i = 0; i < numRows - 1; i++) {
        vector<int> row = results.back();
        row.push_back(1);
        int last = row[0];
        for (int j = 1; j < row.size() - 1; j++) {
            int tmp = row[j];
            row[j] += last;
            last = tmp;
        }
        results.push_back(row);
    }
    return results;
}
```

#### 119. Pascal's Triangle II
The same as 118 but easier because you don't have to store the previous results.

```cpp
vector<int> getRow(int rowIndex) {
    if (rowIndex < 0) return vector<int> {};
    vector<int> row = {1};
    for(int i = 0; i < rowIndex; i++) {
        row.push_back(1);
        int last = row[0];
        for (int j = 1; j < row.size() - 1; j++) {
            int tmp = row[j];
            row[j] += last;
            last = tmp;
        }
    }
    return row;
}
```

##### 232. Implement Queue using Stacks
Use two stacks, one major and one secondary. Add new elements into the secondary and pop them to the major one when extracting elements from the class.

```cpp
class Queue {
private:
    queue<int> majorQueue;
    queue<int> secondaryQueue;
public:
    // Push element x to the back of queue.
    void push(int x) {
        secondaryQueue.push(x);
        if (majorQueue.empty() && !secondaryQueue.empty()) swapContent();
    }

    // Removes the element from in front of queue.
    void pop(void) {
        if (!majorQueue.empty()) majorQueue.pop();
        if (majorQueue.empty() && !secondaryQueue.empty()) swapContent();
    }

    // Get the front element.
    int peek(void) {
        if (!majorQueue.empty()) return majorQueue.front();
        else return -1;
    }

    // Return whether the queue is empty.
    bool empty(void) {
        return majorQueue.empty() && secondaryQueue.empty();
    }

    void swapContent(void) {
        while (!secondaryQueue.empty()) {
            majorQueue.push(secondaryQueue.front());
            secondaryQueue.pop();
        }
    }
};
```

##### 26. Remove Duplicates from Sorted Array
Haven't I done the same one before? See 27.

```cpp
int removeDuplicates(vector<int>& nums) {
    int counter = 0;
    int last = INT_MAX;
    for(int i = 0; i < nums.size(); i++) {
        if (nums[i] != last) {
            nums[counter++] = nums[i];
            last = nums[i];
        }
    }
    return counter;
}
```

##### 172. Factorial Trailing Zeroes
Basically, it depends on how many `5` exisits in the factors. So divide it by five till none left.

```cpp
int trailingZeroes(int n) {
    if (n < 1) return 0;
    int zeroCount = 0;
    while (n > 4) {
        zeroCount += n/5;
        n /= 5;
    }
    return zeroCount;
}
```

##### 21. Merge Two Sorted Lists
The code is kinda ugly but whatever, it works. Just link the next one to the smaller node in the two lists.

```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    if (l1 == NULL && l2 == NULL) return NULL;
    if (l1 == NULL) return l2;
    if (l2 == NULL) return l1;

    ListNode* head = NULL;
    if (l1->val < l2->val) {
        head = l1;
        l1 = l1->next;
    } else {
        head = l2;
        l2 = l2->next;
    }
    ListNode* tail = head;

    while (l1 != NULL && l2 != NULL) {
        if (l1->val < l2->val) {
            tail->next = l1;
            l1 = l1->next;
        } else {
            tail->next = l2;
            l2 = l2->next;
        }
        tail = tail->next;
    }
    while (l1 != NULL) {
        tail->next = l1;
        l1 = l1->next;
        tail = tail->next;
    }
    while (l2 != NULL) {
        tail->next = l2;
        l2 = l2->next;
        tail = tail->next;
    }
    return head;
}
```

##### 66. Plus One
Keep adding till no temp is left.

```cpp
vector<int> plusOne(vector<int>& digits) {
    int tmp = 1;
    int i = digits.size() - 1;
    while (tmp && i > -1) {
        int sum = tmp + digits[i];
        digits[i] = sum%10;
        tmp = sum/10;
        i--;
    }
    if (tmp) {
        digits.insert(digits.begin(), tmp);
    }
    return digits;
}
```

##### 102. Binary Tree Level Order Traversal
It seems like the previous one, except no reverse in the end.

```cpp
vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> results;
    vector<int> rowResults;
    queue<TreeNode*> bfsQueue;
    queue<TreeNode*> tmpQueue;
    if(root != NULL) bfsQueue.push(root);
    while (!bfsQueue.empty()) {
        TreeNode* tmpNode = bfsQueue.front();
        bfsQueue.pop();
        rowResults.push_back(tmpNode->val);
        if(tmpNode->left != NULL) tmpQueue.push(tmpNode->left);
        if(tmpNode->right != NULL) tmpQueue.push(tmpNode->right);
        if (bfsQueue.empty() && !tmpQueue.empty()) {
            swap(bfsQueue, tmpQueue);
            results.push_back(rowResults);
            rowResults.clear();
        }
    }
    if(!rowResults.empty()) results.push_back(rowResults);
    return results;
}
```

##### 36. Valid Sudoku
Just check each column, row and block.

```cpp
class Solution {
public:
    const int SIZE = 9;
    const int BLOCK_SIZE = 3;
    const int NUM_BLOCK = 3;
    bool isValidSudoku(vector<vector<char>>& board) {
        for (int i = 0; i < SIZE; i++) {
            int myMap[9] = {0};
            for (int j = 0; j < SIZE; j++) {
                if (board[i][j] != '.') {
                    if (myMap[board[i][j] - '1']) return false;
                    else myMap[board[i][j] - '1'] = 1;
                }
            }
        }
        for (int i = 0; i < SIZE; i++) {
            int myMap[9] = {0};
            for (int j = 0; j < SIZE; j++) {
                if (board[j][i] != '.') {
                    if (myMap[board[j][i] - '1']) return false;
                    else myMap[board[j][i] - '1'] = 1;
                }
            }
        }
        for (int k = 0; k < NUM_BLOCK; k++) {
            for (int l = 0; l < NUM_BLOCK; l++) {
                int myMap[9] = {0};
                for (int i = k*BLOCK_SIZE; i < (k+1)*BLOCK_SIZE; i++) {
                    for (int j = l*BLOCK_SIZE; j < (l+1)*BLOCK_SIZE; j++) {
                        if (board[j][i] != '.') {
                            if (myMap[board[j][i] - '1']) return false;
                            else myMap[board[j][i] - '1'] = 1;
                        }
                    }
                }
            }
        }
        return true;
    }
};
```

##### 9. Palindrome Number
Convert it to string, I don't care.

```cpp
bool isPalindrome(int x) {
    string str = to_string(x);
    string ori(str);
    reverse(str.begin(), str.end());
    return str == ori;
}
```

##### 110. Balanced Binary Tree
From each node, check its left and right heights. Use dfs to get maximum height.

```cpp
bool isBalanced(TreeNode* root) {
    return dfsHeight(root, 0) != -1;
}
int dfsHeight(TreeNode* node, int height) {
    if (node == NULL) return height;
    int lh = dfsHeight(node->left, height+1);
    int rh = dfsHeight(node->right, height+1);
    if (lh == -1 || rh == -1 || abs(lh - rh) > 1) return -1;
    else return max(lh, rh);
}
```

##### 111. Minimum Depth of Binary Tree
BFS will do nicely. Use a for loop with queue size for each level.

```cpp
int minDepth(TreeNode* root) {
    queue<TreeNode*> bfsQueue, tmpQueue;
    if (root != NULL) bfsQueue.push(root);
    int level;
    while (!bfsQueue.empty()) {
        level++;
        int N = bfsQueue.size();
        for (int i = 0; i < N; i++) {
            TreeNode* node = bfsQueue.front();
            bfsQueue.pop();
            if (node->left == NULL && node->right == NULL) return level;
            if (node->left != NULL) bfsQueue.push(node->left);
            if (node->right != NULL) bfsQueue.push(node->right);
        }
    }
    return 0;
}
```

##### 257. Binary Tree Paths
Use dfs to find each path. Add it to result vector when a leaf is reached.

```cpp
class Solution {
private:
    vector<string> allPath;
public:
    vector<string> binaryTreePaths(TreeNode* root) {
        if (root != NULL) {
            string base = to_string(root->val);
            if (root->left == NULL && root->right == NULL)
                allPath.push_back(base);
            else {
                dfsGetPaths(root->left, base);
                dfsGetPaths(root->right, base);
            }
        }
        return allPath;
    }

    void dfsGetPaths(TreeNode* node, string str) {
        if (node == NULL) return;
        str += "->" + to_string(node->val);
        if (node->left == NULL && node->right == NULL) {
            allPath.push_back(str);
        } else {
            dfsGetPaths(node->left, str);
            dfsGetPaths(node->right, str);
        }
    }
};
```

##### 205. Isomorphic Strings

Essentially, build two maps from one map to another (isomorphically) and then check if there is any mismatch. Below is a nice, concise implementation from online discussion.

```cpp
bool isIsomorphic(string s, string t) {
    int cs[128] = {0}, ct[128] = {0};
    for(int i=0; i < s.size(); i++) {
        if(cs[s[i]] != ct[t[i]]) return false;
        else if(!cs[s[i]] && !ct[t[i]]) {
            cs[s[i]] = i+1;
            ct[t[i]] = i+1;
        }
    }
    return true;
}
```

##### 223. Rectangle Area

Find the areas of the two rectangles and subtract the overlapping area from their sum.

```cpp
bool isIsomorphic(string s, string t) {
    int cs[128] = {0}, ct[128] = {0};
    for(int i=0; i < s.size(); i++)
    {
        if(cs[s[i]] != ct[t[i]]) return false;
        else if(!cs[s[i]] && !ct[t[i]]) //only record once
        {
            cs[s[i]] = i+1;
            ct[t[i]] = i+1;
        }
    }
    return true;
}
```

##### 19. Remove Nth Node From End of List

Move one till the end with the other one n nodes behind it. Then move that node. Take care of the edge cases.

 ```cpp
 ListNode* removeNthFromEnd(ListNode* head, int n) {
    if (head == NULL) return head;
    ListNode* tail = head;
    ListNode* ntail = head;
    for (int i = 0; i < n + 1; i++) {
        if (tail == NULL) return head->next;
        tail = tail->next;
    }
    while (tail!=NULL) {
        tail = tail->next;
        ntail = ntail->next;
    }
    ntail->next = ntail->next->next;
    return head;
}
```

##### 290. Word Pattern

This is very similar to 205. Instead of creating an isomorphical map between two characters, create a map between a char and a string.

```cpp
bool wordPattern(string pattern, string str) {
    vector<string> splitStr = splitBySpace(str);
    unordered_map<char, string> map1;
    unordered_map<string, char> map2;
    if(pattern.size() != splitStr.size()) return false;
    for (int i = 0; i < pattern.size(); i++) {
        if (map1.find(pattern[i]) == map1.end() && map2.find(splitStr[i]) == map2.end()) {
            map1[pattern[i]] = splitStr[i];
            map2[splitStr[i]] = pattern[i];
        } else {
            if (map1[pattern[i]] != splitStr[i]) return false;
            if (map2[splitStr[i]] != pattern[i]) return false;
        }
    }
    return true;
}
vector<string> splitBySpace(string str) {
    vector<string> tokens;
    string delim = " ";
    size_t prev = 0, pos = 0;
    do{
        pos = str.find(delim, prev);
        if (pos == string::npos) pos = str.length();
        string token = str.substr(prev, pos-prev);
        if (!token.empty()) tokens.push_back(token);
        prev = pos + delim.length();
    } while (pos < str.length() && prev < str.length());
    return tokens;
}
```

##### 160. Intersection of Two Linked Lists
Let two nodes travel to the end and then switch to the other node. When they meet, it is the intersection. Below is a nice implementation from online.

```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
    ListNode *cur1 = headA, *cur2 = headB;
    while (cur1 != cur2) {
        cur1 = cur1 ? cur1->next : headB;
        cur2 = cur2 ? cur2->next : headA;
    }
    return cur1;
}
```

##### 88. Merge Sorted Array
Similar to merge two linked list. Instead of merging from the head, merge from the tail to do everything in place.

```cpp
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
    int r1 = m - 1, r2 = n - 1;
    for(int i = m + n - 1; i > -1 && r1 > -1 && r2 > -1; i--) {
        int tmp;
        if (nums1[r1] < nums2[r2]) {
            tmp = nums2[r2--];
        } else {
            tmp = nums1[r1--];
        }
        nums1[i] = tmp;
    }
    while (r2 > -1) {
        nums1[r2] = nums2[r2--];
    }
}
```

##### 219. Contains Duplicate II
Keep a hashset for the `k` elements in between and check if there are any duplicates.

```cpp
bool containsNearbyDuplicate(vector<int>& nums, int k) {
    unordered_set<int> map;
    for(int i = 0; i < k && i < nums.size(); i++) {
        if(map.find(nums[i]) != map.end()) return true;
        else map.insert(nums[i]);
    }
    for(int i = k; i < nums.size(); i++) {
        if(map.find(nums[i]) != map.end()) return true;
        else {
            map.insert(nums[i]);
            map.erase(nums[i-k]);
        }
    }
    return false;
}
```

##### 38. Count and Say
Count and say, literally. Just do the strings right.

```cpp
string countAndSay(int n) {
    if (n < 1) return "";
    string result = "1";
    for (int i = 1; i < n; i++){
        result = nextSequence(result);
    }
    return result;
}
string nextSequence(const string& str) {
    string nextStr = "";
    char tmp = str[0];
    int count = 1;
    for(int i = 1; i < str.size(); i++) {
        if (str[i] != tmp) {
            if (count) {
                nextStr += to_string(count) + string(1, tmp);
                count = 1;
                tmp = str[i];
            }
        } else {
            count++;
        }
    }
    nextStr += to_string(count) + string(1, tmp);
    return nextStr;
}
```

##### 20. Valid Parentheses
Use a stack to keep track of the last parenthesis and see if the next one will match.

```cpp
bool isValid(string s) {
    stack<char> lastPar;
    for(int i = 0; i < s.size(); i++) {
        if(s[i] == '(' || s[i] == '{' || s[i] == '[') {
            lastPar.push(s[i]);
        } else {
            if (lastPar.empty()) return false;
            else if (lastPar.top() != (s[i] - 2) && lastPar.top() != (s[i] - 1)) return false;
            else lastPar.pop();
        }
    }
    if(lastPar.empty()) return true;
    else return false;
}
```

##### 234. Palindrome Linked List
Reverse the linked list in the middle and check if the list is palindrome from both sides.

```cpp
bool isPalindrome(ListNode* head) {
    if (head == NULL) return true;
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast != NULL) {
        fast = fast->next;
        if (fast != NULL) fast = fast->next;
        else break;
        slow = slow->next;
    }
    ListNode* last = slow;
    slow = slow->next;
    last->next = NULL;
    while (slow != NULL) {
        ListNode* tmp = slow->next;
        slow->next = last;
        last = slow;
        slow = tmp;
    }

    while(head != NULL && last != NULL) {
        if(head->val != last->val) return false;
        head = head->next;
        last = last->next;
    }
    return true;
}
```

##### 58. Length of Last Word
Forget fancy functions, just count from the back and ignore irrelevant characters. Do it the simple way.

```cpp
int lengthOfLastWord(string s) {
    int i = s.size() - 1;
    int counter = 0;
    while (i > -1) {
        if (s[i--] != ' ') counter++;
        else if (counter) return counter;
    }
    return counter;
}
```

##### 203. Remove Linked List Elements
Do it in place, just link the next element. Make sure to skip all repeating elements in a row.

```cpp
ListNode* removeElements(ListNode* head, int val) {
    while (head != NULL && head->val == val) head = head->next;
    ListNode* tail = head;
    while (tail != NULL) {
        while (tail->next != NULL && tail->next->val == val) {
                tail->next = tail->next->next;
        }
        tail = tail->next;
    }
    return head;
}
```

##### 225. Implement Stack using Queues
Use a circular queue to implement stack. (Implementing stack using queue is a BAD idea.)

```cpp
class Stack {
private:
    queue<int> circularQueue;
public:
    // Push element x onto stack.
    void push(int x) {
        circularQueue.push(x);
        for (int i = 0; i < (circularQueue.size() - 1); i++) {
            circularQueue.push(circularQueue.front());
            circularQueue.pop();
        }
    }

    // Removes the element on top of the stack.
    void pop() {
        circularQueue.pop();
    }

    // Get the top element.
    int top() {
        if (!circularQueue.empty()) return circularQueue.front();
        else return -1;
    }

    // Return whether the stack is empty.
    bool empty() {
        return circularQueue.empty();
    }
};
```

##### 14. Longest Common Prefix
Just check each string and get the longest common prefix from each comparison.

```cpp
string longestCommonPrefix(vector<string>& strs) {
    if (strs.empty()) return "";
    string lcp = strs[0];
    for (int i = 1; i < strs.size(); i++) lcp = findLcp(lcp, strs[i]);
    return lcp;
}
string findLcp(string str1, string str2) {
    string tmpLcp = "";
    for(int i = 0; i < min(str1.size(), str2.size()); i++) {
        if (str1[i] == str2[i]) {
            tmpLcp += str1[i];
        } else break;
    }
    return tmpLcp;
}
```

##### 303. Range Sum Query - Immutable
Make a partial sum array first. DP.

```cpp
class NumArray {
private:
    vector<int> arrayPartialSum;
public:
    NumArray(vector<int> &nums) {
        arrayPartialSum = nums;
        for (int i = 1; i < nums.size(); i++) {
            arrayPartialSum[i] = nums[i] + arrayPartialSum[i-1];
        }
        arrayPartialSum.insert(arrayPartialSum.begin(), 0);

    }

    int sumRange(int i, int j) {
        return arrayPartialSum[j + 1] - arrayPartialSum[i];
    }
};
```

##### 1. Two Sum
Classy. Use a map.

```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> existingNums;
    for (int i = 0; i < nums.size(); i++) {
        int comp = target - nums[i];
        if (existingNums.find(comp) != existingNums.end()) return vector<int> {existingNums[comp], i};
        else existingNums[nums[i]] = i;
    }
    return vector<int> {};
}
```

##### 125. Valid Palindrome
This one is really annoying. There is a nice function `isalnum` to quickly check if a char is letter or number. (I can't believe c++ doesn't have a `to_lower` for strings!)

```cpp
bool isPalindrome(string s) {
    int i = 0, j = s.size() - 1;
    while (i < j) {
        while (!isalnum(s[i]) && i < j) i++;
        while (!isalnum(s[j]) && i < j) j--;
        if (tolower(s[i++]) != tolower(s[j--]))
            return false;
    }
    return true;
}
```

##### 155. Min Stack
Have a stack that also keeps track of the smallest number "so far". When a number is popped, the minima associated the rest elements should not change.

```cpp
class MinStack {
struct NumPair {
    int num;
    int curMin;
    NumPair(int n, int m) {
        num = n;
        curMin = m;
    }
};
private:
    stack<NumPair> numStack;
public:
    /** initialize your data structure here. */
    MinStack() {
    }

    void push(int x) {
        NumPair tmp(x, min(x,this->getMin()));
        numStack.push(tmp);
    }

    void pop() {
        if (!numStack.empty()) return numStack.pop();
    }

    int top() {
        if (!numStack.empty()) return numStack.top().num;
        else return -1;
    }

    int getMin() {
        if (!numStack.empty()) return numStack.top().curMin;
        else return INT_MAX;
    }
};
```

## Medium

##### 381. Insert Delete GetRandom O(1) - Duplicates allowed

Have a vector for quick random number generation and then have map that keeps track of the element position in the vector for quick deletion. When deleting, remove the element by swapping it with the last element. To achieve this, the vector element should also know how to refer back to the map so that swapping two elements in the vector will update its change to the map as well.

```cpp
class RandomizedCollection {
private:
    // randomList.first = val, .second = index to refer back to multimap
    vector<pair<int, int>> randomList;
    // dataMap.key = val, .val = indices in randomList
    unordered_map<int, vector<int>> dataMap;
public:
    /** Initialize your data structure here. */
    RandomizedCollection() {
        srand(unsigned(time(0)));
    }

    /** Inserts a value to the collection. Returns true if the collection did not already contain the specified element. */
    bool insert(int val) {
        auto ret = dataMap.find(val) == dataMap.end();
        dataMap[val].push_back(randomList.size());
        randomList.push_back(pair<int, int>(val, dataMap[val].size() - 1));
        return ret;
    }

    /** Removes a value from the collection. Returns true if the collection contained the specified element. */
    bool remove(int val) {
        if (dataMap.find(val) == dataMap.end()) return false;
        auto backElement = randomList.back();
        dataMap[backElement.first][backElement.second] = dataMap[val].back();
        randomList[dataMap[val].back()] = backElement;
        randomList.pop_back();
        dataMap[val].pop_back();
        if(dataMap[val].empty()) dataMap.erase(val);
        return true;
    }

    /** Get a random element from the collection. */
    int getRandom() {
        return randomList[rand() % randomList.size()].first;
    }
};
```

##### 355. Design Twitter
Nothing crazy, just have good OO design is important. When using the map, it is important to have the default constructor and copy constructor. When a new constructor is defined, the default (implicitly defined) constructors will not be implemented by the compiler.

This algorithm can be optimized by using a `priority_queue` to find the newest 10 tweets instead of sorting the whole array. The test cases are not big enough for significant improvement on this (it will even slow down the overal performance). Also use `make_heap` can provide finer control than the `priority_queue`.

```cpp
struct Tweet {
    int content;
    int time;
    Tweet();
    Tweet(const int content, const int time) {
        this->content = content;
        this->time = time;
    }
    Tweet(const Tweet& t) {
        this->content = t.content;
        this->time = t.time;
    }
};

inline bool cmpTweet(Tweet a, Tweet b) {
    return a.time > b.time;
}

struct User {
    vector<Tweet> tweets;
    unordered_set<int> followingUserIdGroup;
    User() {};
    User(const int content, const int time) {
        post(content, time);
    }
    User(const int followingUserId) {
        followingUserIdGroup.insert(followingUserId);
    }
    User(const User& user) {
        this->tweets = user.tweets;
        this->followingUserIdGroup = user.followingUserIdGroup;
    }
    void post(const int content, const int time) {
        tweets.push_back(Tweet(content, time));
    }
    void follow(const int followingUserId) {
        followingUserIdGroup.insert(followingUserId);
    }
    void unfollow(const int unfollowingUserId) {
        followingUserIdGroup.erase(unfollowingUserId);
    }
};

class Twitter {
private:
    int timeId;
    unordered_map<int, User> db;
public:
    /** Initialize your data structure here. */
    Twitter() {
        timeId = 0;
    }

    /** Compose a new tweet. */
    void postTweet(int userId, int tweetId) {
        if (db.find(userId) != db.end()) {
            db[userId].post(tweetId, timeId);
        } else {
            User tmpUser = User(tweetId, timeId);
            tmpUser.follow(userId);
            db[userId] = tmpUser;
        }
        timeId++;
    }

    /** Retrieve the 10 most recent tweet ids in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user herself. Tweets must be ordered from most recent to least recent. */
    vector<int> getNewsFeed(int userId) {
        vector<Tweet> allTweets;
        if (db.find(userId) != db.end()) {
            User user = db[userId];
            for (int uid : user.followingUserIdGroup) {
                vector<Tweet> tmpTweets = db[uid].tweets;
                allTweets.insert(allTweets.end(), tmpTweets.begin(), tmpTweets.end());
            }
        }
        sort(allTweets.begin(), allTweets.end(), cmpTweet);
        vector<int> newsFeed;
        for(int i = 0; i < min((int)allTweets.size(), 10); i++) {
            newsFeed.push_back(allTweets[i].content);
        }
        return newsFeed;
    }

    /** Follower follows a followee. If the operation is invalid, it should be a no-op. */
    void follow(int followerId, int followeeId) {
        if (db.find(followerId) != db.end()) {
            db[followerId].follow(followeeId);
        } else {
            User tmpUser = User(followeeId);
            tmpUser.follow(followerId);
            db[followerId] = tmpUser;
        }
    }

    /** Follower unfollows a followee. If the operation is invalid, it should be a no-op. */
    void unfollow(int followerId, int followeeId) {
        if (followerId == followeeId) return;
        if (db.find(followerId) != db.end()) {
            db[followerId].unfollow(followeeId);
        }
    }
};
```

##### 300. Longest Increasing Subsequence

Use basic dp idea. For each number, check its previous longest subsequence and store the value. For each new element, check the longest possible subsquence to form from the previous data. Then, just return the biggest number in the array.

Possible optimization to make the solution o(nlog(n)): instead of marking every number, keep a vector of maximum subsequence and associated largest number. This way, a larger subsequence can only be made if the new number is larger than the associated largest number. This way, a binary search will be used to determine the max length associated with this new number. Necessary update will be made to the vector when the new max length can be made with smaller tail element. (It's too annoying to implement the binary search here so I didn't implement it.)

 ```cpp
 int lengthOfLIS(vector<int>& nums) {
    vector<pair<int, int>> maximumLengthDP;
    for (int i = 0; i < nums.size(); i++) {
        int maxLength = 1;
        for (int j = 0; j < maximumLengthDP.size(); j++) {
            if (maximumLengthDP[j].first < nums[i]) maxLength = max(maxLength, maximumLengthDP[j].second + 1);
        }
        maximumLengthDP.push_back(make_pair(nums[i], maxLength));
    }
    int maxLen = 0;
    for (int i = 0; i < maximumLengthDP.size(); i++) {
        maxLen = max(maxLen, maximumLengthDP[i].second);
    }
    return maxLen;
}
```

##### 136. Single Number
Simple dirty trick - Xor operatory.

```cpp
int singleNumber(vector<int>& nums) {
    int result = 0;
    for (int i = 0; i < nums.size(); i++) {
        result ^= nums[i];
    }
    return result;
}
```


##### 338. Counting Bits
Find the pattern. Each \[2^n, 2^(n+1)\] segment is the \[0, 2^n\] plus one.

```cpp
vector<int> countBits(int num) {
    if (num < 0) return vector<int> {};
    int N = ceil(log2(num));
    vector<int> allBits = {0};
    for (int i = 0; i < N + 1; i++) {
        allBits = expand(allBits);
    }
    vector<int> partBits(allBits.begin(), allBits.begin() + num + 1);
    return partBits;
}
vector<int> expand(vector<int> oldVec) {
    vector<int> newVec(oldVec);
    for (int i = 0; i < oldVec.size(); i++) {
        oldVec[i] += 1;
    }
    newVec.insert(newVec.end(), oldVec.begin(), oldVec.end());
    return newVec;
}
```

##### 122. Best Time to Buy and Sell Stock II
Sell when the price is at a local maximum.

```cpp
int maxProfit(vector<int>& prices) {
    if (prices.empty()) return 0;
    int curMin = prices[0];
    int curMax = prices[0];
    int sum = 0;
    for (int i = 0; i < prices.size(); i++) {
        if (prices[i] < prices[i - 1]) {
            sum += curMax - curMin;
            curMin = prices[i];
            curMax = prices[i];
        } else {
            curMin = min(curMin, prices[i]);
            curMax = max(curMax, prices[i]);
        }
    }
    sum += curMax - curMin;
    return sum;
}
```

##### 357. Count Numbers with Unique Digits
I think a math formula can be derived. Not super interesting, implementation comes from online discussion.

```cpp
int countNumbersWithUniqueDigits(int n) {
    int ans = 10, tmp = 9;
    for(int i = 1; i < n && tmp; ++i) ans += (tmp *= (10-i));
    return n ? ans : 1;
}
```

##### 343. Integer Break
Use dynamic programming. Break an integer into two parts and multiply them to get the possible maximum. Note that the registered maximum should be the greater one of 1. the largest product and 2. the number itself. E.g., 2 can only have 1 as its maximum breakdown product but it does not have to be broken down when it's used as a part of 3.

```cpp
int integerBreak(int n) {
    vector<int> dp(n, 1);
    for(int i = 1; i < n; i++) {
        int M = ceil((i + 1)/2);
        int maxProd = 1;
        for(int j = 0; j < M; j++) {
            maxProd = max(maxProd, dp[j] * dp[i - j - 1]);
        }
        if (i == (n - 1)) return maxProd;
        dp[i] = max(maxProd, i + 1);
    }
    return dp[n-1];
}
```

##### 319. Bulb Switcher
There is a mathematical argument behind the results. I'm not too interested.

```cpp
int bulbSwitch(int n) {
    return sqrt(n);
}
```

##### 144. Binary Tree Preorder Traversal
Use a stack to do dfs.

```cpp
vector<int> preorderTraversal(TreeNode* root) {
    vector<int> valList;
    stack<TreeNode*> dfsStack;
    dfsStack.push(root);
    while (!dfsStack.empty()) {
        int N = dfsStack.size();
        for (int i = 0; i < N; i++) {
            TreeNode* tmp = dfsStack.top();
            dfsStack.pop();
            if (tmp != NULL) {
                dfsStack.push(tmp->right);
                dfsStack.push(tmp->left);
                valList.push_back(tmp->val);
            }
        }
    }
    return valList;
}
```

##### 378. Kth Smallest Element in a Sorted Matrix
I used a linear search, basically iterate through the smallest set that contains all the candidates. But a smarter move would be to do a binary search given that the matrix is sorted.

Linear search:

```cpp
int kthSmallest(vector<vector<int>>& matrix, int k) {
    priority_queue<int> kQueue;
    int N = matrix.size();
    int M = ceil((float) k / N);
    int L = ceil(sqrt(k));
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            kQueue.push(matrix[i][j]);
            if (kQueue.size() > k) kQueue.pop();
        }
    }
    for (int i = M; i < N; i++) {
        for (int j = 0; j < M; j++) {
            kQueue.push(matrix[i][j]);
            if (kQueue.size() > k) kQueue.pop();
        }
    }
    for (int i = M; i < L; i++) {
        for (int j = M; j < L; j++) {
            kQueue.push(matrix[i][j]);
            if (kQueue.size() > k) kQueue.pop();
        }
    }
    return kQueue.top();
}
```

Binary search (from online discussion):

```cpp
int kthSmallest(vector<vector<int>>& matrix, int k)
{
    int size = matrix.size(), l = matrix[0][0], r = matrix[size-1][size-1];
    while(l < r)
    {
        int smaller = 0, m = l+((r-l)>>1);
        for(int i = 0; i < size; ++i)
            smaller += upper_bound(matrix[i].begin(), matrix[i].end(), m)-matrix[i].begin();
        smaller < k ? l = m + 1 : r = m;
    }
    return r;
}
```

##### 384. Shuffle an Array
I'm not sure what's going on with this one, just shuffle it and return each time.

```cpp
class Solution {
private:
    vector<int> ori;
    vector<int> shuffled;
public:
    Solution(vector<int> nums) {
        ori = nums;
        shuffled = nums;
    }

    /** Resets the array to its original configuration and return it. */
    vector<int> reset() {
        return ori;
    }

    /** Returns a random shuffling of the array. */
    vector<int> shuffle() {
        random_shuffle(shuffled.begin(), shuffled.end());
        return shuffled;
    }
};
```

##### 238. Product of Array Except Self
The central idea is to have partial product both in the left and in the right, then multiply them together. I did by modifying the original array. But a smarter way will do everything in place.

Basic, no extra space:

```cpp
vector<int> productExceptSelf(vector<int>& nums) {
    vector<int> prodVec(nums.size(), 1);
    for (int i = 1; i < nums.size(); i++) {
        prodVec[i] = prodVec[i - 1] * nums[i - 1];
    }
    int last = 1;
    for (int i = nums.size() - 1; i > -1; i--) {
        int tmp = last * nums[i];
        nums[i] = last;
        last = tmp;
    }
    for (int i = 0; i < nums.size(); i++) {
        prodVec[i] = prodVec[i] * nums[i];
    }
    return prodVec;
}
```

In-place version

```cpp
vector<int> productExceptSelf(vector<int>& nums) {
    int n = nums.size();
    vector<int> output(n, 1);
    int front = 1;
    int end = 1;
    for (int i = 0; i < n-1; i++) {
        front *= nums[i];
        end *= nums[n-1-i];
        output[i+1] *= front;
        output[n-2-i] *= end;
    }
    return output;
}
```

##### 347. Top K Frequent Elements
Use a map counter to count each distinct elements. Then use a priority_queue to get the kth most frequent in the collection.

NOTE: remember to get the default constructor for struct.

```cpp
struct NumWithCounter {
    int num;
    int counter;
    NumWithCounter();
    NumWithCounter(int n, int c) {
        num = n;
        counter = c;
    }
};

struct CmpNum {
    inline bool operator() (NumWithCounter a, NumWithCounter b) {
        return a.counter > b.counter;
    }
};

class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> mapCounter;
        for (int i = 0; i < nums.size(); i++) {
            if (mapCounter.find(nums[i]) != mapCounter.end()) {
                mapCounter[nums[i]]++;
            } else {
                mapCounter[nums[i]] = 1;
            }
        }
        priority_queue<NumWithCounter, vector<NumWithCounter>, CmpNum> kHighNum;
        for (auto element : mapCounter) {
            kHighNum.push(NumWithCounter(element.first, element.second));
            if (kHighNum.size() > k) {
                kHighNum.pop();
            }
        }
        vector<int> ret;
        while (!kHighNum.empty()) {
            ret.push_back(kHighNum.top().num);
            kHighNum.pop();
        }
        return ret;
    }
};
```

## Hard

##### 146. LRU Cache
Use a hash map and doubly linked list to implement the problem. Possible optimization: implement a more light-weight singly linked list to store the order.

```cpp
class LRUCache{
private:
    int cap;
    int size;
    list<int> keyOrderList;
    unordered_map<int, pair<list<int>::iterator, int>> cache;
public:
    LRUCache(int capacity) {
        cap = capacity;
        size = 0;
    }

    int get(int key) {
        if(cache.find(key) == cache.end()) return -1;
        pair<list<int>::iterator, int> valuePair = cache[key];
        keyOrderList.erase(valuePair.first);
        keyOrderList.push_front(key);
        cache[key].first = keyOrderList.begin();
        return valuePair.second;
    }

    void set(int key, int value) {
        if(get(key) != -1) {
            cache[key].second = value;
        } else {
            if(size >= cap) {
                cache.erase(keyOrderList.back());
                keyOrderList.pop_back();
                size--;
            }
            keyOrderList.push_front(key);
            cache[key] = make_pair(keyOrderList.begin(), value);
            size++;
        }
    }
};
```
