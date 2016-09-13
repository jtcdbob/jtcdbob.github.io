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
        else if (--counter < 0) {
			popularElement = nums[i];
			counter = 1;
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
        int nodeFound = 0;
        if (root->val == p->val) nodeFound += 1;
        if (root->val == q->val) nodeFound += 1;
        nodeFound += left + right;
        if (nodeFound == 2) {
            lca = root;
            nodeFound = -1;
        }
        return nodeFound;
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
Nothing much, just plain bfs traversal. Make sure to keep track of the elements in each level. This can be done by using two queues. Alternatively, use a `for` loop each time going into the queue.

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
This one is really annoying. There is a nice function `isalnum()` to quickly check if a char is letter or number. (I can't believe c++ doesn't have a `to_lower()` for strings!)

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

##### 94. Binary Tree Inorder Traversal
Use dfs to go through the tree.

```cpp
vector<int> inorderTraversal(TreeNode* root) {
    vector<int> results;
    TreeNode* cur = root;
    TreeNode* pre = NULL;
    while (cur != NULL) {
        if (cur->left != NULL) {
            pre = cur->left;
            while (pre->right != NULL && pre->right != cur) {
                pre = pre->right;
            }
            if (pre->right == NULL) {
                pre->right = cur;
                cur = cur->left;
            } else {
                pre->right = NULL;
                results.push_back(cur->val);
                cur = cur->right;
            }
        } else {
            results.push_back(cur->val);
            cur = cur->right;
        }
    }
    return results;
}
```

##### 387. First Unique Character in a String
Use a map to keep track of all uniquely existing letters in a string, then return the one with smallest index.

```cpp
int firstUniqChar(string s) {
    vector<int> mapFirstIndex(26, -2);
    for (int i = 0; i < s.size(); i++) {
        const int letter = s[i]-'a';
        if (mapFirstIndex[letter] == -2) {
            mapFirstIndex[letter] = i;
        } else {
            mapFirstIndex[letter] = -1;
        }
    }
    int minIndex = INT_MAX;
    for (int i = 0; i < mapFirstIndex.size(); i++) {
        if (mapFirstIndex[i] > -1) {
            minIndex = min(minIndex, mapFirstIndex[i]);
        }
    }
    return minIndex < INT_MAX ? minIndex : -1;
}
```

##### 388. Longest Absolute File Path
Keep the length of directory at each level. When a file is found, return the total length from root to the end. Another language with better string parsing library is probably better for this problem.

```cpp
int lengthLongestPath(string input) {
    vector<int> folderLength(1, 0);
    int head = 0;
    int maxLength = 0;
    while (head < input.size()) {
        int tail = head;
        int tier = 1;
        bool isFile = false;
        while (input[tail] != '\n' && tail < input.size()) {
            if (input[tail] == '\t') tier++;
            if (input[tail] == '.') isFile = true;
            tail++;
        }
        int pathLength = tail - head - tier + 1;
        if (isFile) {
            pathLength += folderLength[tier - 1];
            maxLength = max(maxLength, pathLength);
        } else {
            int folderPathLength = folderLength[tier - 1] + pathLength + 1;
            if (folderLength.size() < tier + 1) {
                folderLength.push_back(folderPathLength);
            } else {
                folderLength[tier] = folderPathLength;
            }
        }
        head = tail + 1;
    }
    return maxLength;
}
```

##### 236. Lowest Common Ancestor of a Binary Tree
Use dfs to go through the tree and find matching nodes. The first node that has two matching nodes in its subtree is the lowest common ancestor. Note that matching node is done by `node1 == node2` not `node1->val == node2->val` because there is no gaurantee on uniqueness of the values.

```cpp
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    lca = NULL;
    dfsFindNodes(root, p, q);
    return lca;
}
int dfsFindNodes(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (root == NULL) return 0;
    int numFound = 0;

    int leftFound = dfsFindNodes(root->left, p, q);
    if (leftFound < 0) return -1;
    else numFound += leftFound;

    int rightFound = dfsFindNodes(root->right, p, q);
    if (rightFound < 0) return -1;
    else numFound += rightFound;

    if (root == p || root == q) numFound++;

    if (numFound == 2) {
        lca = root;
        numFound = -1;
    }
    return numFound;
}
```

A more concise solution from online.

```cpp
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root || root == p || root == q) return root;
    TreeNode* left = lowestCommonAncestor(root->left, p, q);
    TreeNode* right = lowestCommonAncestor(root->right, p, q);
    return !left ? right : !right ? left : root;
}
```

##### 86. Partition List
Use two dummy heads, go through the list and reorder. Remember to truncate the tail of both lists or the new list may have a loop in itself.

```cpp
ListNode* partition(ListNode* head, int x) {
    ListNode *h1 = new ListNode(0), *h2 = new ListNode(0);
    ListNode *t1 = h1, *t2 = h2;
    ListNode *tail = head;
    while (tail) {
        if (tail->val < x) {
            t1->next = tail;
            t1 = t1->next;
        } else {
            t2->next = tail;
            t2 = t2->next;
        }
        tail = tail->next;
    }
    t2->next = NULL;
    t1->next = h2->next;
    return h1->next;
}
```

##### 230. Kth Smallest Element in a BST
Use in-order traversal to visit the tree nodes and return the kth element visted. The solution is strange - I can't return the value after finding it without getting a runtime error.

```cpp
int kthSmallest(TreeNode* root, int k) {
    TreeNode* node = root;
    TreeNode* tmp = NULL;
    int counter = 0;
    int ret = -1;
    while (node != NULL) {
        if (node->left != NULL) {
            tmp = node->left;
            while (tmp->right != NULL && tmp->right != node) {
                tmp = tmp->right;
            }
            if (tmp->right == node) {
                tmp->right = NULL;
                if (++counter == k) ret = node->val;
                node = node->right;
            } else {
                tmp->right = node;
                node = node->left;
            }
        } else {
            if (++counter == k) ret = node->val;
            node = node->right;
        }
    }
    return ret;
}
```

##### 94. Binary Tree Inorder Traversal
The same as `230`. Use Morris traversal to visit the tree with o(1) space and o(n) time. This is also doable with a stack - store the current node and then the left node.

##### 284. Peeking Iterator
Add a new method `peak()` in the subclass and let the compiler do all the work to inherit the rest methods.

```cpp
int peek() {
    return Iterator{*this}.next();
}
```

##### 199. Binary Tree Right Side View
Use BFS to visit each level and add the last\(rightmost) to the return vector.

```cpp
vector<int> rightSideView(TreeNode* root) {
    vector<int> results;
    queue<TreeNode*> bfsQueue;
    if (root != NULL) bfsQueue.push(root);
    while (!bfsQueue.empty()) {
        int curLevelSize = bfsQueue.size();
        int tmp;
        for (int i = 0; i < curLevelSize; i++) {
            TreeNode* node = bfsQueue.front();
            tmp = node->val;
            if (node->left != NULL) bfsQueue.push(node->left);
            if (node->right != NULL) bfsQueue.push(node->right);
            bfsQueue.pop();
        }
        results.push_back(tmp);
    }
    return results;
}
```

##### 153. Find Minimum in Rotated Sorted Array
The trick is to know that even though the array is rotated, its subsequences are still monotonic. Unlike binary search, it has four possible scenarios. List them all and the algorithm is similar to that of binary search.

```cpp
int findMin(vector<int>& nums) {
    int l = 0, r = nums.size() - 1;
    if (nums[r] >= nums[l]) return nums[l];
    while (l + 1 < r) {
        int m = (int) (l + r) / 2;
        if (nums[m] > nums[l]) l = m;
        else r = m;
    }
    return min(nums[l], nums[r]);
}
```

##### 62. Unique Paths
This is a high school math problem. The key is to compute factorial efficiently. Use type `long` to avoid overflow and divide from the smaller element to avoid dividing by nonexistent factors.

```cpp
int uniquePaths(int m, int n) {
    long M = max(m - 1, n - 1), N = min(m - 1, n - 1);
    if (!M | !N) return 1;
    long prod = 1;
    for (long i = M + N; i > M; i--) {
        prod *= i;
        prod /= (M + N + 1 - i);
    }
    return prod;
}
```

##### 173. Binary Search Tree Iterator
This is in-order traversal. Use a stack to do it. The structure will use this algorithm. I believe Morris traversal can be implemented too if wanted.

```cpp
class BSTIterator {
private:
    stack<TreeNode*> inOrderStack;
public:
    BSTIterator(TreeNode *root) {
        TreeNode* tail = root;
        while (tail != NULL) {
            inOrderStack.push(tail);
            tail = tail->left;
        }
    }

    /** @return whether we have a next smallest number */
    bool hasNext() {
        return !inOrderStack.empty();
    }

    /** @return the next smallest number */
    int next() {
        TreeNode* node = inOrderStack.top();
        inOrderStack.pop();
        TreeNode* tail = node->right;
        while (tail != NULL) {
            inOrderStack.push(tail);
            tail = tail->left;
        }
        return node->val;
    }
};
```

##### 34. Search for a Range
I got lazy and called stock function. But essentially it's a bunch of binary search and then find the lower/upper bounds.

```cpp
vector<int> searchRange(vector<int>& nums, int target) {
    if (find(nums.begin(), nums.end(), target) == nums.end()) return vector<int> {-1, -1};
    int l = lower_bound(nums.begin(), nums.end(), target) - nums.begin();
    int r = upper_bound(nums.begin(), nums.end(), target) - nums.begin() - 1;
    return vector<int> {l, r};
}
```

##### 49. Group Anagrams
Sort each string and use that as a hash key. Alternatively, one can compute the hash more elegantly \(after all, only 26 letters are used in this case). One idea from online discussion is to multiply prime numbers with individual characters, that will make the hash.

Straightforward one, let `unordered_map` do the hashing for you.

```cpp
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    vector<vector<string>> results;
    unordered_map<string, int> myMap;
    for (string str : strs) {
        string tmp(str);
        sort(tmp.begin(), tmp.end());
        if (myMap.find(tmp) != myMap.end()) {
            results[myMap[tmp]].push_back(str);
        } else {
            myMap[tmp] = results.size();
            results.push_back(vector<string> {str});
        }
    }
    return results;
}
```

This one uses prime numbers to hash the string:

```cpp
class Solution {
private:
vector<int> primes = {2, 3, 5, 7, 11 ,13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 107};
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<int,int> map;
        vector<vector<string> >result;
        int count=1;
        for(auto i : strs){
            int hash = 1;
//using hash function instead of sort & caching index in map
            for(int j=0; j < i.size(); ++j){
                hash *= primes[i[j]-'a'];
            }
            if(map[hash] == 0){
                vector<string> cur(1);
                cur[0] = i;
                result.push_back(cur);
                map[hash] = count++;
           }
            else
            result[map[hash]-1].push_back(i);
        }
        return result;
    }
};
```

##### 92. Reverse Linked List II

Use a dummy head and go to \(m-1)th node. Then keep track of the node head in the middle as well as the tail node. Reverse everything in between. Lastly, stitch the middle part with two ends to finish.

```cpp
ListNode* reverseBetween(ListNode* head, int m, int n) {
    ListNode* dummyHead = new ListNode(0);
    dummyHead->next = head;

    ListNode* midHead = dummyHead;
    for (int i = 0; i < m - 1; i++) midHead = midHead->next;
    ListNode* midTail = midHead;
    ListNode* tail = midTail->next;
    for (int i = m - 1; i < n; i++) {
        ListNode* tmp = tail->next;
        tail->next = midTail;
        midTail = tail;
        tail = tmp;
    }
    midHead->next->next = tail;
    midHead->next = midTail;

    return dummyHead->next;
}
```


##### 55. Jump Game
A typical DP problem. Keep track of the maximum length one can jump and keep adding to it. Once it's impossible to keep going, return false; otherwise, return true at the end.

```cpp
bool canJump(vector<int>& nums) {
    int maxLength = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (i > maxLength) return false;
        maxLength = max(nums[i] + i, maxLength);
    }
    return true;
}
```

##### 207. Course Schedule
This is a graph problem. Essentially, one wants to find out whether there exists a loop in the graph. Kahn's algorithm uses DFS to traverse the graph. Use colored node to help implement this algorithm.

My implementation of Kahn's algorithm based on my memory.

```cpp
bool canFinish(int numCourses, vector<pair<int, int>>& prerequisites) {
    vector<int> courseList(numCourses, 1); // Node color marker
    vector<vector<int>> prereqList(numCourses, vector<int> {}); // graph in matrix rep.
    for (const auto& prereq : prerequisites) {
        courseList[prereq.second] = 0; // Mark node white if it has exit
        prereqList[prereq.first].push_back(prereq.second); // Register matrix entries
    }
    for (int i = 0; i < numCourses; i++) {
        // Start from black nodes
        if (courseList[i]) {
            stack<int> visitedNodes;
            visitedNodes.push(i);
            while (!visitedNodes.empty()) {
                int curNode = visitedNodes.top();
                if (courseList[curNode] < 0) return false; // Encountered grey nodes => a loop
                if (!prereqList[curNode].empty()) {
                    courseList[curNode] = -1; // Mark grey
                    visitedNodes.push(prereqList[curNode].back()); // Visit the next prereq
                    prereqList[curNode].pop_back();
                } else {
                    courseList[curNode] = 1; // No more prereq, mark black, finished
                    visitedNodes.pop(); // Go back
                    if (!visitedNodes.empty()) courseList[visitedNodes.top()] = 0; // Mark the last one white again
                }
            }
        }
    }
    for (int i = 0; i < numCourses; i++) {
        if (courseList[i] < 1) return false; // Non-black node exists ==> a loop;
    }
    return true;
}
```

A faster version from online discussion. Similar idea, but instead of tracking individual node, this one just speed through the entire graph and see if all nodes are adequately visited. Very good implementation.

```cpp
bool canFinish(int numCourses, vector<pair<int, int>>& prerequisites) {
    vector<vector<int>> graph(numCourses);
    vector<int> indegree(numCourses,0);
    for(auto edge : prerequisites) {
        graph[edge.second].push_back(edge.first);
        ++indegree[edge.first];
    }
    queue<int> Q;
    for(int i = 0;i < numCourses;i++)
        if(indegree[i] == 0)
            Q.push(i);
    int counter = 0;
    while(!Q.empty()) {
        int u = Q.front();
        Q.pop();
        ++counter;
        for(auto v : graph[u]) {
            if(--indegree[v] == 0)
                Q.push(v);
        }
    }
    return counter == numCourses;
}
```

##### 373. Find K Pairs with Smallest Sums
Use minStack to get the kth smallest pair. Alternatively, you can get all the pairs and sort them. My minStack implementation is even slower than the sort version. Not clear what I did wrong on a language level. Here is a version from online discussion that is better (lots of new tricks here too):

```cpp
vector<pair<int, int>> kSmallestPairs(vector<int> & nums1, vector<int> & nums2, int k) {
    vector<pair<int,int>> v;
    if(nums1.empty() || nums2.empty()) return v;
    auto cmp = [&nums1, &nums2](const pair<int, int> & a, const pair<int, int> &b) {
        return nums1[a.first]+nums2[a.second] > nums1[b.first]+nums2[b.second]; };
    priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(cmp)> minHeap(cmp);
    minHeap.emplace(0, 0);
    while(minHeap.size() && k--) {
        auto t = minHeap.top(); minHeap.pop();
        v.emplace_back(nums1[t.first], nums2[t.second]);
        if(t.first < nums1.size()-1) minHeap.emplace(t.first + 1, t.second);
        if(t.first == 0 && t.second < nums2.size() - 1) minHeap.emplace(t.first, t.second + 1);
    }
    return v;
}
```

##### 187. Repeated DNA Sequences
The idea is to find a quick way to keep track of the DNA sequence of length 10. A nice hash function will do this fast. Alternatively, use a hashset and let it do the hash for you. This implementation is from online discussion that uses bit manipulation to do the hash dirty fast. Note that there are only four letters, so it's just actually hashing four elements in combination.

Side note on the hash using bit manipulation. As discussed, it is really not that many elements that are different ("A, C, G, T"), and someone discovered that they have two bits that are distinct, so they did some bit manipulation to get that out fast. The same can be done using a swtich statement to change char to int (it will do the same with minor performance hit).

```cpp
vector<string> findRepeatedDnaSequences(string s) {
    char flag[262144] ={0};
    vector<string> result;
    int len,DNA=0,i;
    if((len=s.length()) < 11) return result;
    for(i = 0 ; i < 9; i++)
        DNA = DNA << 2 | (s[i] - 'A' + 1) % 5;
    for(i = 9; i < len; i++) {
        DNA = (DNA << 2 & 0xFFFFF)|(s[i] - 'A' + 1) % 5;
            if(!(flag[DNA >> 2] & (1 << ((DNA & 3) << 1))))
                flag[DNA >> 2] | = (1 << ((DNA & 3) << 1));
            else if(!(flag[DNA >> 2] & (2 << ((DNA & 3) << 1)))) {
                result.push_back(s.substr(i - 9, 10));
                flag[DNA >> 2] |= (2 << ((DNA & 3) << 1));
            }
    }
    return result;
}
```

##### 17. Letter Combinations of a Phone Numbe
Really nothing here. List all and add to the existing combo.

```cpp
class Solution {
private:
    vector<string> numToChar = {" ", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
public:
    vector<string> letterCombinations(string digits) {
        if (digits.empty()) return vector<string> {};
        vector<string> results = {""};
        for (int i = 0; i < digits.size(); i++) {
            int num = digits[i] - '0';
            vector<string> tmp;
            string newStr = numToChar[num];
            for (const char& c : newStr) {
                for (string s : results) {
                    tmp.push_back(s.append(1, c));
                }
            }
            results.swap(tmp);
        }
        return results;
    }
};
```

##### 392. Is Subsequence
Keep a pointer to the last matched letter in string s and move the pointer to the right while going through the string t. If the pointer reaches the end, there exists a subsequence, otherwise not.

```cpp
bool isSubsequence(string s, string t) {
    if (s.empty()) return true;
    int i = 0, j = 0;
    while (i < s.size() && j < t.size()) {
        if (s[i] == t[j++]) i++;
    }
    return i == s.size();
}
```

##### 328. Odd Even Linked List
Use two dummy heads to do it. Make sure to terminate the even node after the last one. If the list has odd number of nodes, there is a chance for inifinite loop if the tail is not properly cut.

```cpp
ListNode* oddEvenList(ListNode* head) {
    ListNode *oHead = new ListNode(0);
    ListNode *eHead = new ListNode(0);
    ListNode *oTail = oHead, *eTail = eHead;
    ListNode *tail = head;
    while(tail != NULL) {
        oTail->next = tail;
        oTail = oTail->next;
        tail = tail->next;
        eTail->next = tail;
        eTail = eTail->next;
        if (tail != NULL) tail = tail->next;
    }
    oTail->next = eHead->next;
    return oHead->next;
}
```

##### 377. Combination Sum IV
Use dynamic programming for this problem.

```cpp
int combinationSum4(vector<int>& nums, int target) {
    vector<int> dpArray(target + 1, 0);
    dpArray[0] = 1;
    sort(nums.begin(), nums.end());
    for(int i = 1; i < dpArray.size(); i++) {
        int dpSum = 0;
        for(int j = 0; j < nums.size(); j++) {
            if ((i - nums[j]) < 0) break;
            else dpSum += dpArray[i - nums[j]];
        }
        dpArray[i] = dpSum;
    }
    return dpArray.back();
}
```

##### 337. House Robber III
Use dfs to traverse the tree and have a dynamic programming backbone to the algorithm.

```cpp
int rob(TreeNode* root) {
    if (root == NULL) return 0;
    int maxProf1 = rob(root->left) + rob(root->right);
    int maxProf2 = root->val;
    maxProf2 += getChildrenSum(root->left);
    maxProf2 += getChildrenSum(root->right);
    root->val = max(maxProf1, maxProf2);
    return root->val;
}

/* Helper function */
int getChildrenSum(TreeNode* node) {
    int sum = 0;
    if (node != NULL) {
        if (node->left != NULL) sum += node->left->val;
        if (node->right != NULL) sum += node->right->val;
    }
    return sum;
}
```

##### 167. Two Sum II - Input array is sorted
Move from left and right ends and find the target. This is a linear method with constant space. Tried binary search, but it's too annoying.

```cpp
vector<int> twoSum(vector<int>& numbers, int target) {
    int l = 0, r = numbers.size() - 1;
    while(l < r) {
        int sum = numbers[l] + numbers[r];
        if(sum > target) r--;
        else if (sum < target) l++;
        else return vector<int> {l + 1, r + 1};
    }
    return vector<int> {};
}
```

##### 260. Single Number III
Sort, I'm not patient with bit operations.

```cpp
vector<int> singleNumber(vector<int>& nums) {
    vector<int> res;
    sort(nums.begin(), nums.end());
    for(int i = 0; i < nums.size();) {
        if (i + 1 >= nums.size()) res.push_back(nums[i++]);
        else if (nums[i] != nums[i + 1]) res.push_back(nums[i++]);
        else i += 2;
    }
    return res;
}
```

For reference, this is a solution with bit operation:

```cpp
vector<int> singleNumber(vector<int>& nums) {
    int aXorb = 0;  // the result of a xor b;
    for (auto item : nums) aXorb ^= item;
    int lastBit = (aXorb & (aXorb - 1)) ^ aXorb;  // the last bit that a diffs b
    int intA = 0, intB = 0;
    for (auto item : nums) {
        // based on the last bit, group the items into groupA(include a) and groupB
        if (item & lastBit) intA = intA ^ item;
        else intB = intB ^ item;
    }
    return vector<int>{intA, intB};
}
```

##### 318. Maximum Product of Word Lengths
We want quick comparision of two strings for the same letters used. Use a bit map to do it quickly.

```cpp
int maxProduct(vector<string>& words) {
    vector<int> flagArray(words.size(), 0);
    int N = words.size();
    for (int i = 0; i < N; i++) {
        for (char l : words[i]) {
            flagArray[i] |= (1 << (l - 'a'));
        }
    }
    int maxSize = 0;
    for (int i = 0; i < N; i++) {
        int a = words[i].size();
        for (int j = i + 1; j < N; j++) {
            if (!(flagArray[i] & flagArray[j])) {
                int b = words[j].size();
                maxSize = max(maxSize, a * b);
            }
        }
    }
    return maxSize;
}
```

##### 382. Linked List Random Node
Use [reservoir sampling](https://en.wikipedia.org/wiki/Reservoir_samplin) technique for the algorithm.

```cpp
class Solution {
private:
    ListNode* head;
public:
    Solution(ListNode* head) {
        this->head = head;
    }
    int getRandom() {
        int count = 1;
        ListNode* tail = head;
        int res=0;
        while(tail != NULL) {
            int n = rand() % count;
            if(n==0) res = tail->val;
            tail = tail->next;
            count++;
        }
        return res;
    }
};
```
##### 114. Flatten Binary Tree to Linked List
Traverse the tree using a stack for dfs.

```cpp
void flatten(TreeNode* root) {
    stack<TreeNode*> dfsStack;
    TreeNode* tail = new TreeNode(0);
    if (root != NULL) dfsStack.push(root);
    while (!dfsStack.empty()) {
        TreeNode* tmp = dfsStack.top();
        dfsStack.pop();
        if (tmp->right != NULL) dfsStack.push(tmp->right);
        if (tmp->left != NULL) dfsStack.push(tmp->left);
        tail->left = NULL;
        tail->right = tmp;
        tail = tail->right;
    }
}
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

#####
