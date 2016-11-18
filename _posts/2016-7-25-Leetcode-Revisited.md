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

##### 204. Count Primes
Basic algorithm (The Sieve of Eratosthenes), note the limit for update cells. For best performance (for large number cases), use array instead of vector for light-weight structure:

```cpp
int countPrimes(int n) {
    bool numList[n];
    memset(numList, true, sizeof(numList));
    for (int i = 3; i * i < n; i++) {
        if (numList[i]) {
            for (int j = i * i; j < n; j += (2 * i)) {
                numList[j] = false;
            }
        }
    }
    int counter = 0;
    for (int i = 3; i < n; i += 2) {
        if (numList[i]) counter++;
    }
    return counter + (n > 2);
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

Here is a dirty trick:

```cpp
bool isPowerOfTwo(int n) {
    if (n <= 0) return false;
    return !(n & (n - 1));
}
```

So the `!(n & (n - 1))` is unique to power of 2, but for general number `n`, just use `pow(n, m) / num` to see if `num` is a power of `n`. `m` should be chosen so that the large number is right about to overflow `int`.

##### 342. Power of Four
Well, just do log, I don't care.

```cpp
bool isPowerOfFour(int num) {
    if (num == 5 || num < 1) return false;
    double ans = log(num) / log(4);
    return round(ans) == ans;
}
```

Here is another dirty trick:

```cpp
bool isPowerOfFour(int num) {
    return (num > 0) && !(num & (num - 1)) && ((num & 0x55555555) == num);
}
```

`0x55555555` is basically `0101 0101 ..... 0101`.

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

##### 113. Path Sum II

Relatively easy, just do dfs and keep track of each element along the path, when a sum is found, push back the path track to the result set.

```cpp
vector<vector<int>> pathSum(TreeNode* root, int sum) {
    vector<vector<int>> res;
    vector<int> tmp;
    dfsFindPath(root, sum, res, tmp);
    return res;
}
void dfsFindPath(TreeNode* node, int sum, vector<vector<int>>& results, vector<int>& tmp) {
    if (node == NULL) return;
    tmp.push_back(node->val);
    sum -= node->val;
    if (node->left == NULL && node->right == NULL && sum == 0) {
        results.push_back(tmp);
    } else {
        if (node->left != NULL) dfsFindPath(node->left, sum, results, tmp);
        if (node->right != NULL) dfsFindPath(node->right, sum, results, tmp);
    }
    tmp.pop_back();
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

##### 409. Longest Palindrome

Very straightforward question - just count how many each letter has shown up in the string. Say if 'a' has shown up 3 times, then we can at least use 2 'a's on both ends of the new palindrome. Then if we have letter that is odded out, we can add it to the center (only once). The performance of this algorithm can be improved by using more suitable data structure and stuffs, but hey I wrote it in 3 min.

```cpp
int longestPalindrome(string s) {
    unordered_map<char, int> countDict;
    for (char c : s) {
        if (countDict.find(c) != countDict.end()) countDict[c]++;
        else countDict[c] = 1;
    }
    int counter = 0, oddFlag = 0;
    for (auto pair : countDict) {
        int isOdd = pair.second % 2;
        counter += pair.second - isOdd;
        oddFlag += isOdd;
    }
    return counter + (oddFlag > 0);
}
```

##### 441. Arranging Coins

Easy math formula derived from n*(n+1) > 2k. Do cast to (double) for better performance and avoid round errors.

```cpp
int arrangeCoins(int n) {
    return (sqrt(1.0 + 8.0 * n) - 1.0 ) / 2.0;
}
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
Use dfs to go through the tree. Alternatively, there is a method that uses o(n) time and o(1) space. Morris traversal:

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

##### 45. Jump Game II

Keep track of the maximum jump distance and only update the jump count when you exceed that point. Helpful [discussion](https://discuss.leetcode.com/topic/57368/evolve-from-brute-force-to-optimal).

```cpp
int jump(vector<int>& nums) {

    int maxDist = 0, curMax = 0, jumpCount = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (i > curMax) {
            jumpCount ++;
            curMax = maxDist;
        }
        maxDist = max(maxDist, i + nums[i]);
    }
    return jumpCount;
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

##### 15. 3Sum

Remember that when the array is sorted, there are faster way to go through the problem without using extra space. Now 3Sum is just the same problem with extra layer of loop. Using a hashmap sort of works (o(n^2)) but the space complexity is not good enough.

Note the inner loop is actually working on the section left to the outer index. This skips the duplicate comfortably (I didn't write this), nice approach:

```cpp
vector<vector<int>> threeSum(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    vector<vector<int>> ans;
    for (int k = 2; k < nums.size(); k++) {
        if (k + 1 < nums.size() && nums[k] == nums[k + 1]) continue; // Skip duplicates
        int i = 0, j = k - 1;
        int target = 0 - nums[k];
        while (i < j) {
            int sum = nums[i] + nums[j];
            if (sum < target || (i > 0 && nums[i - 1] == nums[i])) i++; // Skip duplicates
            else if (sum > target || (j + 1 < k && nums[j] == nums[j + 1]))j--; // Skip duplicates
            else ans.push_back({nums[i++], nums[j--], nums[k]});
        }
    }
    return ans;
}
```

##### 16. 3Sum Closest

Similar to 3 sum. Instead of finding the exact target number, see if each time the sum gets closer to the target number. Structure of the code is the same as 15 but the core logics changes a little bit.

```cpp
int threeSumClosest(vector<int>& nums, int target) {
    sort(nums.begin(), nums.end());
    int closeSum = 0;
    int dist = INT_MAX;
    for (int k = 2; k < nums.size(); k++) {
        if (k + 1 < nums.size() && nums[k] == nums[k + 1]) continue;
        int i = 0, j = k - 1;
        int newTarget = target - nums[k];
        while (i < j) {
            int sum = nums[i] + nums[j];
            int tmpDist = abs(sum - newTarget);
            if (tmpDist < dist) {
                dist = tmpDist;
                closeSum = nums[i] + nums[j] + nums[k];
            }
            if (sum < newTarget) i++;
            else if (sum > newTarget) j--;
            else return target;

            while (i > 0 && nums[i - 1] == nums[i]) i++;
            while (j + 1 < k && nums[j] == nums[j + 1]) j--;
        }
    }
    return closeSum;
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
Use [reservoir sampling](https://en.wikipedia.org/wiki/Reservoir_sampling) technique for the algorithm. The basic idea is to keep one element while going through the entire list of unknown length. For ith element in the list, give it 1/i probability to replace the element and eventually just return that element. The probability that any element is kept in the end is then `1/n`, where `n` is hitherto unknown length of the list.

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

##### 200. Number of Islands
Use the recursive method to label every visited island. Note that this is not an efficient approach. A more sophisticated method will use one sweep to label points and then associate the points with groups before taking a second pass to relabel the points in groups. In this case, the second pass is not needed because we only care about the total number.

```cpp
int numIslands(vector<vector<char>>& grid) {
    int count = 0;
    for (int i = 0; i < grid.size(); i++) {
        for (int j = 0; j < grid[0].size(); j++) {
            count += dfsLabel(grid, i, j);
        }
    }
    return count;
}
int dfsLabel(vector<vector<char>>& grid, int x, int y) {
    if (grid[x][y] == '0') return 0;
    grid[x][y] ='0';
    if (x < grid.size() - 1) dfsLabel(grid, x + 1, y);
    if (y < grid[0].size() - 1) dfsLabel(grid, x, y + 1);
    if (x > 0) dfsLabel(grid, x - 1, y);
    if (y > 0) dfsLabel(grid, x, y - 1);
    return 1;
}
```

##### 22. Generate Parentheses
Use recursion, end when there are no more parenthesis to add and then push back the generated string to the result vector.

```cpp
class Solution {
    vector<string> result;
public:
    vector<string> generateParenthesis(int n) {
        string s = "";
        addPar(s, n, n);
        return result;
    }
    void addPar(string str, int l, int r) {
        if (l > r) return;
        if (!l && !r) result.push_back(str);
        else {
            if (l > 0) addPar(str + "(", l - 1, r);
            if (r > 0) addPar(str + ")", l, r - 1);
        }
    }
};
```

##### 108. Convert Sorted Array to Binary Search Tree
It is similar to the idea of merge sort (divide and conquer?). Split the sorted array into two and then build a tree using that.

```cpp
TreeNode* sortedArrayToBST(vector<int>& nums) {
    return recursiveBuild(nums, 0, nums.size());
}
TreeNode* recursiveBuild(vector<int>& nums, int l, int r) {
    if (l >= r) return NULL;
    int m = floor((l + r) / 2);
    TreeNode* root = new TreeNode(nums[m]);
    root->left = recursiveBuild(nums, l, m);
    root->right = recursiveBuild(nums, m + 1, r);
    return root;
}
```

##### 96. Unique Binary Search Trees
This is more of a math problem then a programming one. Note that when there are $$n$$ numbers, if $$k$$ is the root, there are $$k-1$$ possible combination in its left tree and $$n-k$$ possibilities in its right tree. So the total number of combination for $$n$$ numbers is the sum $$\sum_{i=0}^n A(i - 1) A(n - i)$$. Knowing this, it is easy to come up with a dynamic programming model to solve the problem.

```cpp
int numTrees(int n) {
    if (n < 1) return 0;
    vector<int> dpArray(n + 1, 1);
    for (int i = 2; i < n + 1; i++) {
        int combo = 0;
        for (int j = 0; j < i; j++) {
            combo += dpArray[j] * dpArray[i - j - 1];
        }
        dpArray[i] = combo;
    }
    return dpArray.back();
}
```

##### 394. Decode String
Be systematic with the decoding. C++ is unlikely the best language to do this kind of string manipulation.

```cpp
string decodeString(string s) {
    int l = 0;
    string decodedStr = "";
    while(l < s.size()) {
        if (s[l] <= '9' && s[l] >= '0') decodedStr += decode(s, l);
        else decodedStr += s[l++];
    }
    return decodedStr;
}

string decode(const string& s, int &l) {
    int r = l;
    int n;
    string subStr, ret;
    // Get repetition number
    while (s[r] <= '9' && s[r] >= '0') r++;
    n = stoi(s.substr(l, r++));
    // Get substring enclosed by []
    while(s[r] != ']') {
        if (s[r] <= '9' && s[r] >= '0') subStr += decode(s, r);
        else subStr += s[r++];
    }
    // Make new substring for return;
    for (int i = 0; i < n; i++) ret += subStr;
    // Update l
    l = ++r;
    return ret;
}
```

##### 309. Best Time to Buy and Sell Stock with Cooldown
Dynamic programming. Before selling, always compare it to possible outcome when not doing any sale. A naive implementation:

```cpp
int maxProfit(vector<int>& prices) {
    if (prices.empty()) return 0;
    vector<int> dpMaxArrayVal(prices.size(), 0);
    vector<int> dpMaxArrayHold(prices.size(), 0);
    dpMaxArrayVal[1] = max(0, prices[1] - prices[0]);
    for (int i = 2; i < prices.size(); i++) {
        int curPrice = prices[i];
        int maxDif = 0;
        for (int j = 0; j < i; j++) {
            maxDif = max(maxDif, curPrice - prices[j] + dpMaxArrayHold[j]);
        }
        dpMaxArrayVal[i] = max(maxDif, dpMaxArrayVal[i - 1]);
        dpMaxArrayHold[i] = dpMaxArrayVal[i - 2];
    }
    return dpMaxArrayVal.back();
}
```

Someone online took another step and used four `int` to deal with the dynamic model and eliminated space and time waste (note this is a linear algorithm):


```cpp
int maxProfit(vector<int>& prices) {
    int buy(INT_MIN), sell(0), prev_sell(0), prev_buy;
    for (int price : prices) {
        prev_buy = buy;
        buy = max(prev_sell - price, buy);
        prev_sell = sell;
        sell = max(prev_buy + price, sell);
    }
return sell;
```

##### 216. Combination Sum III
Use dynamic programming to do this. For n, it can only increase numbers in n-1 results. Make sure to eliminate the duplicate before moving on.

```cpp
vector<vector<int>> combinationSum3(int k, int n) {
    // Filter out some impossible inputs
    const int LOW = k * (k + 1) / 2;
    if (n < LOW) return vector<vector<int>>{};

    // Initialize DP
    vector<int> base = vector<int> (k);
    for (int i = 0; i < k; i++) base[i] = i + 1;
    vector<vector<int>> collection = {base};

    // DP body
    for (int i = LOW; i < n; i++) {
        vector<vector<int>> new_collection;
        for (vector<int> comb : collection) {
            for (int j = 0; j < k - 1; j++) {
                vector<int> tmp = comb;
                if (tmp[j] + 1 < tmp[j + 1]) {
                    tmp[j]++;
                    new_collection.push_back(tmp);
                }
            }
            if (++comb[k - 1] < 10) new_collection.push_back(comb);
        }
        // Remove duplicate results
        swap(collection, new_collection);
        sort(collection.begin(), collection.end());
        collection.erase(unique(collection.begin(), collection.end()), collection.end());
    }
    return collection;
}
```

##### 137. Single Number II
Not very interested, sort.

```cpp
int singleNumber(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    int l = 0;
    while (l < nums.size()) {
        if (l + 1 < nums.size() && l + 2 < nums.size()) {
            if (nums[l] != nums[l + 1] || nums[l] != nums[l + 2]) return nums[l];
        } else return nums[l];
        l += 3;
    }
    return -1;
}
```

A "real" solution and a discussion on a [generic solution](https://discuss.leetcode.com/topic/22821/an-general-way-to-handle-all-this-sort-of-questions/2) to all these problems:

```cpp
int singleNumber(vector<int>& nums) {
    int ones = 0, twos = 0;
    for(int i = 0; i < nums.size(); i++){
        ones = (ones ^ nums[i]) & ~twos;
        twos = (twos ^ nums[i]) & ~ones;
    }
    return ones;
}
```

##### 241. Different Ways to Add Parentheses
Pretty annoying problem. Didn't get to finish the code. Here is one from online discussion:

```cpp
vector<int> diffWaysToCompute(string input) {
    if(input.size() ==0) return {};
    vector<int> result;
    for(int i = 0; i < input.size(); i++)
    {
        if(input[i]!='+' &&input[i]!= '-' &&input[i]!= '*') continue;
        auto vec1 = diffWaysToCompute(input.substr(0, i));
        auto vec2 = diffWaysToCompute(input.substr(i+1));
        for(auto val1: vec1)
        {
            for(auto val2: vec2)
            {
                if(input[i]=='+') result.push_back(val1+ val2);
                else if(input[i]=='-') result.push_back(val1 - val2);
                else if(input[i]== '*') result.push_back(val1 * val2);
            }
        }
    }
    return result.empty()?vector<int>{stoi(input)}:result;
}
```

##### 116. Populating Next Right Pointers in Each Node

Use BFS to level traverse the tree and link the nodes.

```cpp
void connect(TreeLinkNode *root) {
    queue<TreeLinkNode*> bfsQueue;
    if (root != NULL) bfsQueue.push(root);
    while (!bfsQueue.empty()) {
        int N = bfsQueue.size();
        TreeLinkNode* tmpNode;
        for (int i = 0; i < N; i++) {
            tmpNode = bfsQueue.front();
            if (tmpNode->left != NULL) bfsQueue.push(tmpNode->left);
            if (tmpNode->right != NULL) bfsQueue.push(tmpNode->right);
            bfsQueue.pop();
            if (!bfsQueue.empty()) tmpNode->next = bfsQueue.front();
        }
        tmpNode->next = NULL;
    }
}
```

##### 334. Increasing Triplet Subsequence

One sweep forward and one sweep backward. The problem with one sweep is to have a barrier that makes the current min/max value too small/large thus blocking the chance to detect possible longer subsequences. Two sweeps overcome this problem.

```cpp
bool increasingTriplet(vector<int>& nums) {
    int curMin = INT_MIN;
    int counter = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] > curMin) {
            curMin = nums[i];
            if (++counter > 2) return true;
        }
    }

    int curMax = INT_MAX;
    counter = 0;
    for (int i = nums.size() - 1; i > -1 ; i--) {
        if (nums[i] < curMax) {
            curMax = nums[i];
            if (++counter > 2) return true;
        }
    }

    return false;
}
```

##### 240. Search a 2D Matrix II

Start from right corner and search (diagonally).

```cpp
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    if (matrix.empty()) return false;
    int M = matrix.size();
    int N = matrix[0].size();

    int i = 0, j = N - 1;
    while (i < M && j > -1) {
        int curElem = matrix[i][j];
        if (target > curElem) i++;
        else if (target < curElem) j--;
        else return true;
    }
    return false;
}
```

##### 53. Maximum Subarray

Use a partial sum to keep track of largest connected sum so far. Update maximum whenever the partial sum gets updated/reset.

```cpp
int maxSubArray(vector<int>& nums) {
    int curMax = INT_MIN;
    int partialSum = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] + partialSum >= 0) {
            partialSum += nums[i];
            curMax = max(curMax, partialSum);
        } else {
            partialSum = 0;
            curMax = max(curMax, nums[i]);
        }
    }
    return curMax;
}
```

##### 367. Valid Perfect Square
`sqrt()`, I don't care. OK, if done properly, a number is a perfect square iff it consists of the sum of consecutive odd numbers.

```cpp
bool isPerfectSquare(int num) {
    double sq = sqrt(num);
    return sq == floor(sq);
}
```

"Better" solution from online discussion:

```cpp
bool isPerfectSquare(int num) {
    int e = 1;
    while(num > 0) {
        num -= e;
        e += 2;
    }
    return num == 0;
}
```

##### 179. Largest Number
Order the number and then concatenate them to get the largest number. Important note when two numbers have the same initial sequences. Just compare the result of them in sequence. Once the comparator is defined, do a sort and then concatenate.

```cpp
inline bool strCmp(string a, string b) {
    return (a + b) > (b + a);
}
string largestNumber(vector<int>& nums) {
    vector<string> numsStr(nums.size());
    for (int i = 0; i < nums.size(); i++) numsStr[i] = to_string(nums[i]);
    sort(numsStr.begin(), numsStr.end(), strCmp);

    if (!numsStr.empty() && numsStr[0] == "0") return "0";
    string ret;
    for (int i = 0; i < nums.size(); i++) ret += numsStr[i];
    return ret;
}
```

##### 89. Gray Code

Find the pattern. Write out the first few `n`'s and get a feeling for what to look for. The code is sort of a verbatim translation of the algorithm.

```cpp
vector<int> grayCode(int n) {
    vector<int> results;
    if (n == 0) return vector<int> {0};
    else if (n > 0) {
        results = grayCode(n-1);
        vector<int> tmp(results.rbegin(), results.rend());
        int bitChangeAt = (1 << (n - 1));
        for (int i = 0; i < tmp.size(); i++) {
            tmp[i] ^= bitChangeAt;
        }
        results.insert(results.end(), tmp.begin(), tmp.end());
    }
    return results;
}
```

##### 59. Spiral Matrix II

I'm doing it the dumb way. Just iterate through the matrix in a spiral.

```cpp
vector<vector<int>> generateMatrix(int n) {
    vector<int> innerTmp(n, 0);
    vector<vector<int>> retMatrix(n, innerTmp);
    int counter = 0;
    int l = 0, r = n, u = 0, d = n;
    while (counter < n*n) {
        for (int i = l; i < r; i++) retMatrix[u][i] = ++counter;
        u++;
        if (counter < n*n) {
            for (int i = u; i < d; i++) retMatrix[i][r - 1] = ++counter;
            r--;
        } else break;
        if (counter < n*n) {
            for (int i = r - 1; i > l - 1; i--) retMatrix[d - 1][i] = ++counter;
            d--;
        }
        if (counter < n*n) {
            for (int i = d - 1; i > u - 1; i--) retMatrix[i][l] = ++counter;
            l++;
        }
    }
    return retMatrix;
}
```

##### 35. Search Insert Position
Just call `lower_bound()`, no reason to skip the function call if it can be easily included. Worst case do a binary search.

```cpp
int searchInsert(vector<int>& nums, int target) {
    return lower_bound(nums.begin(), nums.end(), target) - nums.begin();
}
```

##### 46. Permutations
Again, call a function to do the dirty work for you. I believe there is a dirtier way to do it by examining numbers from the tail (see the other post for code), but I'm not going over it again.

```cpp
vector<vector<int>> permute(vector<int>& nums) {
    vector<vector<int>> results;
    sort(nums.begin(), nums.end());
    do {
        results.push_back(nums);
    } while (next_permutation(nums.begin(), nums.end()));
    return results;
}
```

##### 77. Combinations
The benefit of having a clean function to do the dirty work for you. Just keep track of indices for elements that you want to take to form a combination. This will take the least time.

```cpp
vector<vector<int>> combine(int n, int k) {
    vector<vector<int>> results;
    vector<int> numVec(n, 0);
    vector<int> selectVec(n, 0);
    for (int i = 0; i < n; i++) numVec[i] = i + 1;
    for (int i = n - k; i < n; i++) selectVec[i] = 1;
    do {
        vector<int> tmp(k, 0);
        int counter = 0;
        for (int i = 0; i < n; i++) if (selectVec[i]) tmp[counter++] = numVec[i];
        results.push_back(tmp);
    } while (next_permutation(selectVec.begin(), selectVec.end()));
    return results;
}
```

##### 64. Minimum Path Sum

It is like the dungeon game (174), but easier. Just dp save all the minimum till the end.

```cpp
int minPathSum(vector<vector<int>>& grid) {
    if (grid.empty() || grid[0].empty()) return 0;
    int M = grid.size();
    int N = grid[0].size();

    for (int i = 1; i < M; i++) grid[i][0] += grid[i - 1][0];
    for (int j = 1; j < N; j++) grid[0][j] += grid[0][j - 1];

    for (int i = 1; i < M; i++) {
        for (int j = 1; j < N; j++) {
            grid[i][j] += min(grid[i - 1][j], grid[i][j - 1]);
        }
    }

    return grid[M - 1][N - 1];
}
```

##### 48. Rotate Image
Do it in place by swapping the four elements in the "corner".

```cpp
void rotate(vector<vector<int>>& matrix) {
    int N = matrix.size();
    int l = 0, u = 0, r = N, d = N;
    while (l < r) {
        for (int i = 0; i < r - l - 1; i++) {
            int tmp = matrix[u][l+i];
            matrix[u][l+i]     = matrix[d-i-1][l];
            matrix[d-i-1][l]   = matrix[d-1][r-1-i];
            matrix[d-1][r-1-i] = matrix[u+i][r-1];
            matrix[u+i][r-1]   = tmp;
        }
        l++; u++; r--; d--;
    }
}
```

##### 39. Combination Sum
DFS will proper pruning will do nicely. Make sure sort the array because it is not gauranteed.

```cpp
class Solution {
private:
    vector<vector<int>> results;
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        dfsFillResults(candidates, 0, target, vector<int> {});
        return results;
    }

    void dfsFillResults(const vector<int>& candidates, const int l, int target, vector<int> combo) {
        if (target < 0) return;
        else if (target == 0 && !combo.empty()) results.push_back(combo);
        if (l < candidates.size()) {
            if (candidates[l] > target) return;
            int candidate = candidates[l];
            while (target >= 0) {
                dfsFillResults(candidates, l + 1, target, combo);
                combo.push_back(candidate);
                target -= candidate;
            }
        }
    }
};
```

##### 75. Sort Colors
Bucket sort.

```cpp
void sortColors(vector<int>& nums) {
    vector<int> bucketCounter(3, 0);
    for (int num : nums) bucketCounter[num]++;
    int color = 0;
    int i = 0;
    for (int count : bucketCounter) {
        for (int j = 0; j < count; j++) {
            nums[i++] = color;
        }
        color++;
    }
}
```

##### 215. Kth Largest Element in an Array
I used a heap of size `k`, but it is not the fastest method.

```cpp
int findKthLargest(vector<int>& nums, int k) {
    priority_queue<int, vector<int>, greater<int>> pQueue;
    for (int num : nums) {
        pQueue.push(num);
        if (pQueue.size() > k) pQueue.pop();
    }
    return pQueue.top();
}
```

Quick select will yield a faster result (solution from online discussion):

```cpp
class Solution {
private:
    int partition (vector<int>& nums, int left, int right) {
        swap(nums[left], nums[left + random() % (right - left + 1)]);   // randomly choose a pivot and put it on left position
        int pivot = nums[left], slow = left + 1, fast = left + 1;       // use two pointers to partition: slow and fast

        while (fast <= right) {
            if (pivot < nums[fast]) {
                swap(nums[slow++], nums[fast]);
            }
            fast++;
        }

        swap(nums[left], nums[--slow]);                                 // position pivot
        return slow;                                                    // return pivot position
    }

public:
    int findKthLargest(vector<int>& nums, int k) {
        int l = 0, r = nums.size() - 1;
        k--;

        while (l <= r) {
            int n = partition(nums, l, r);

            if (n == k) { return nums[n]; }
            if (n < k) {
                l = n + 1;
            } else {
                r = n - 1;
            }
        }
        return -1;
    }
};
```

Using C++ function, the method is like

```cpp
int findKthLargest(vector<int>& nums, int k) {
    nth_element(nums.begin(), nums.begin() + k - 1, nums.end(), greater<int>());
    return nums[k - 1];
}
```

##### 78. Subsets
Nothing interesting about this one, just find the pattern and add the array to the results.

```cpp
vector<vector<int>> subsets(vector<int>& nums) {
    vector<vector<int>> combo = vector<vector<int>> {vector<int> {}};
    for (int num : nums) {
        vector<vector<int>> tmp;
        for (vector<int> c : combo) {
            c.push_back(num);
            tmp.push_back(c);
        }
        combo.insert(combo.end(), tmp.begin(), tmp.end());
    }
    return combo;
}
```

##### 74. Search a 2D Matrix
Isn't this the same as before?

```cpp
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    if (matrix.empty()) return false;
    int i = 0, j = matrix[0].size() - 1;
    while (i < matrix.size() && j > -1) {
        if (matrix[i][j] < target) i++;
        else if (matrix[i][j] > target) j--;
        else return true;
    }
    return false;
}
```

##### 129. Sum Root to Leaf Numbers

Get all the numbers using dfs and then add them up.

```cpp
class Solution {
private:
    vector<int> allNums;
public:
    int sumNumbers(TreeNode* root) {
        dfsFindNums(root, "");
        int sum = 0;
        for (int num : allNums) sum += num;
        return sum;
    }
    void dfsFindNums(TreeNode* node, string numStr) {
        if (node == NULL) return;
        numStr += to_string(node->val);
        if (node->left == NULL && node->right == NULL) allNums.push_back(stoi(numStr));
        else {
            dfsFindNums(node->left, numStr);
            dfsFindNums(node->right, numStr);
        }
    }
};
```

##### 376. Wiggle Subsequence
The algorithm is straightforward and get the details right.

```cpp
int wiggleMaxLength(vector<int>& nums) {
    if (nums.empty()) return 0;
    int counter = 0;
    int llast = nums.front(), last = nums.front();
    for (int i = 0; i < nums.size(); i++) {
        while (nums[i] == last && i < nums.size()) i++;
        int num = nums.back();
        if (i < nums.size()) num = nums[i];
        if ((last - llast) * (num - last) <= 0) counter++;
        llast = last;
        last = num;
    }
    return counter + (last != llast);
}
```

##### 279. Perfect Squares

DP solution. There is a mathematical one but I don't care about that. Because the test cases are big, use static to recycle some of the computation.

```cpp
bool isSqure(int n) {
    double result = sqrt(n);
    return result == floor(result);
}
int numSquares(int n) {
    static vector<int> dpArray {0};
    int m = dpArray.size();
    dpArray.resize(max(m, n), 0);
    for (int i = m - 1; i < n; i++) {
        int num = i + 1;
        if (isSqure(num)) dpArray[i] = 1;
        else {
            int l = 0, r = i - 1;
            int minNum = INT_MAX;
            while (l <= r) {
                minNum = min(minNum, dpArray[l++] + dpArray[r--]);
            }
            dpArray[i] = minNum;
        }
    }
    return dpArray[n - 1];
}
```

A better algorithm using DP from online discussion:

```cpp
int numSquares(int n) {
    static vector<int> dp {0};
    int m = dp.size();
    dp.resize(max(m, n+1), INT_MAX);
    for (int i=1, i2; (i2 = i*i)<=n; ++i)
        for (int j=max(m, i2); j<=n; ++j)
            if (dp[j] > dp[j-i2] + 1)
                dp[j] = dp[j-i2] + 1;
    return dp[n];
}
```

##### 80. Remove Duplicates from Sorted Array II
Nothing much happening here since the input array is sorted, just check with the number before and see if it is a duplicate.

```cpp
int removeDuplicates(vector<int>& nums) {
    int counter = 2;
    for (int i = 2; i < nums.size(); i++) if (nums[i] != nums[counter - 2]) nums[counter++] = nums[i];
    return min(counter, (int) nums.size());
}
```

##### 209. Minimum Size Subarray Sum
The question is a bit ambiguous. The subarray has to be consecutive. Use greedy algorithm for this problem - keep a window using two pointers and move them across the array.

```cpp
int minSubArrayLen(int s, vector<int>& nums) {
    int minLen = INT_MAX;
    int l = 0, r = 0;
    int partialSum = 0;
    while (r < nums.size()) {
        partialSum += nums[r++];
        while (l < r && partialSum >= s) {
            minLen = min(minLen, r - l);
            partialSum -= nums[l++];
        }
    }
    return minLen == INT_MAX ? 0 : minLen;
}
```

##### 31. Next Permutation
Not very patient with this.

Well, don't be. The actual solution is

> Starting from the end of array, find the first element e_1 which is less than its following element. Reverse all elements after e_1 and then find the first element (e_2) which is greater than e_1 from these reversed elements. Swap e_1 and e_2.



```cpp
void nextPermutation(vector<int>& nums) {
    next_permutation(nums.begin(), nums.end());
}
```

The actual solution.

```cpp
void nextPermutation(vector<int>& nums) {
    for (int i = nums.size() - 2; i > -1; i--) {
        if (nums[i] < nums[i + 1]) {
            reverse(nums.begin() + i + 1, nums.end());
            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[j] > nums[i]) {
                    int tmp = nums[i];
                    nums[i] = nums[j];
                    nums[j] = tmp;
                    return;
                }
            }
            return;
        }
    }
    reverse(nums.begin(), nums.end());
}
```

##### 11. Container With Most Water

Move from both sides, always move the smaller fence first because it is the only possible way to increase the potential maximum area.

```cpp
int maxArea(vector<int>& height) {
    int l = 0, r = height.size() - 1;
    int maxArea = 0;
    while (l < r) {
        int area = min(height[l], height[r]) * (r - l);
        maxArea = max(maxArea, area);
        if (height[l] >= height[r]) r--;
        else l++;
    }
    return maxArea;
}
```

##### 134. Gas Station
First of all, move from one end to the other, if the sum is greater or equal to 0, it is possible to move around. The best position is to move right after the deepest pit (be aware of the circle).

```cpp
int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
    int gasInTank = 0, minGasInTank = INT_MAX, startIndex = 0;
    for (int i = 0; i < gas.size(); i++) {
        gasInTank += gas[i] - cost[i];
        if (gasInTank < minGasInTank) {
            startIndex = i;
            minGasInTank = min(minGasInTank, gasInTank);
        }
    }
    return gasInTank >= 0 ? (startIndex + 1) % gas.size() : -1;
}
```

##### 73. Set Matrix Zeroes
Use the first zero row as a temporary variable to keep track of the zero columns. It will be easier if I use some helper functions to set the zeros, but whatever ¯\\_(ツ)_/¯

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    if (matrix.empty()) return;
    int M = matrix.size(), N = matrix[0].size();
    int firstZeroRow = -1;
    for (int i = 0; i < M; i++) {
        if (firstZeroRow >= 0) break;
        for (int j = 0; j < N; j++) {
            if (matrix[i][j] == 0) {
                firstZeroRow = i;
            }
        }
    }
    for (int i = firstZeroRow + 1; i < M; i++) {
        int zeroRow = 0;
        for (int j = 0; j < N; j++) {
            if (matrix[i][j] == 0) {
                matrix[firstZeroRow][j] = 0;
                zeroRow = 1;
            }
        }
        if (zeroRow) {
            for (int j = 0; j < N; j++) {
                matrix[i][j] = 0;
            }
        }
    }
    if (firstZeroRow >= 0) {
        for (int j = 0; j < N; j++) {
            if (matrix[firstZeroRow][j] == 0) {
                for (int i = 0; i < M; i++) {
                    matrix[i][j] = 0;
                }
            }
        }
        for (int j = 0; j < N; j++) {
            matrix[firstZeroRow][j] = 0;
        }
    }
}
```

##### 82. Remove Duplicates from Sorted List II
Use a dummy head and a dummy tail to go through Duplicates

```cpp
ListNode* deleteDuplicates(ListNode* head) {
    ListNode* dummyHead = new ListNode(0);
    ListNode* dummyTail = dummyHead;
    ListNode* tail = head;
    while (tail != NULL) {
        if (tail->next != NULL && tail->val == tail->next->val) {
            while (tail->next != NULL && tail->val == tail->next->val) tail = tail->next;
            dummyTail->next = NULL;
        } else {
            dummyTail->next = tail;
            dummyTail = dummyTail->next;
        }
        tail = tail->next;
    }
    return dummyHead->next;
}
```

##### 289. Game of Life
Technically, just keep value of the last row and update row by row. In this case, I use code to mark the cell status after update and do a batch update in the very end.

```cpp
void gameOfLife(vector<vector<int>>& board) {
    if (board.empty()) return;
    int M = board.size(), N = board[0].size();
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            board[i][j] = checkCell(i, j, M, N, board); // Mark the cell status by code
            // 3 for reviving and 4 for killing
        }
    }
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            board[i][j] = updateCell(board[i][j]);
        }
    }
}

int checkCell(int i, int j, int M, int N, vector<vector<int>>& board) {
    int aliveCounter = countAlive(i, j, M, N, board);
    if (board[i][j] == 0) {
        if (aliveCounter == 3) return 3; // To be revived
    } else {
        if (aliveCounter < 2 || aliveCounter > 3) return 4; // To be killed
    }
    return board[i][j]; // Nothing happens
}
int countAlive(int i, int j, int M, int N, vector<vector<int>>& board) {
    int aliveCounter = 0;
    for (int k = -1; k < 2; k++) {
        for (int l = -1; l < 2; l++) {
            aliveCounter += isAlive(i + k, j + l, M, N, board);
        }
    }
    aliveCounter -= board[i][j];
    return aliveCounter;
}
int isAlive(int i, int j, int M, int N, vector<vector<int>>& board) {
    if (i < 0 || i > M - 1 || j < 0 || j > N - 1) return 0; // Out of boundary
    if (board[i][j] == 0 || board[i][j] == 3) return 0; // Dead cell before update
    return 1;
}
int updateCell(int cellStatus) {
    return cellStatus % 2;
}
```

##### 162. Find Peak Element
Bisection. The criteria for update is localized.

```cpp
int findPeakElement(vector<int>& nums) {
   int l = 0, r(nums.size());
    while(l < r){
        int mid = l + (r-l) / 2;
        if(mid == l) break;
        if(nums[mid] > nums[mid-1]) l = mid;
        else r = mid;
    }
    return l;
}
```

##### 274. H-Index
Sort and find. See H-Index II.

##### 275. H-Index II
Use bisection to go through the citation. Update criteria uses the index position and citation counter.

```cpp
int hIndex(vector<int>& citations) {
    if (citations.empty()) return 0;
    int l = 0, r = citations.size();
    if (citations.front() >= citations.size()) return citations.size();
    if (citations.back() < 1) return 0;
    while (l < r - 1) {
        int m = (int) (l + r) / 2;
        if (citations[m] > citations.size() - m) r = m;
        else l = m;
    }
    if (citations[l] >= citations.size() - l) return citations.size() - l;
    else return citations.size() - r;
}
```

##### 313. Super Ugly Number
The basic idea is to use prime number and existing numbers to create more candidates. Line up the candidates and get the first n. But we cannot store all the candidates generated along the way, so we get one candidate a time. Keep an index of the last used element in the existing numbers for each prime number so we can generate candidates on the fly. Be aware that there might be duplicated candidates from different prime numbers - update them at the same time.

```cpp
int nthSuperUglyNumber(int n, vector<int>& primes) {
    vector<int> dpArray(n, 1);
    const int M = primes.size();
    vector<int> index(M, 0);
    vector<int> candidates(primes);
    for (int i = 1; i < n; i++) {
        int minNext = INT_MAX;
        for (int j = 0; j < M; j++) {
            minNext = min(minNext, candidates[j]);
        }
        dpArray[i] = minNext;
        for (int j = 0; j < M; j++) {
            if (candidates[j] == minNext) {
                candidates[j] = primes[j] * dpArray[++index[j]];
            }
        }
    }
    return dpArray.back();
}
```

##### 341. Flatten Nested List Iterator
I think there are better ways, but I just flatten the list in constructor and output them one by one.

```cpp
class NestedIterator {
private:
    vector<NestedInteger> nil;
    int cur;
    vector<int> unfolded;
    int curUnfolded;
    vector<int> unfold(vector<NestedInteger> &nestedList) {
        vector<int> ret;
        for (NestedInteger ni : nestedList) {
            if (ni.isInteger()) ret.push_back(ni.getInteger());
            else {
                vector<int> tmp = unfold(ni.getList());
                ret.insert(ret.end(), tmp.begin(), tmp.end());
            }
        }
        return ret;
    }
public:
    NestedIterator(vector<NestedInteger> &nestedList) {
        nil = nestedList;
        cur = 0;
        curUnfolded = 0;
    }

    int next() {
        if (curUnfolded < unfolded.size()) return unfolded[curUnfolded++];
        if (nil[cur].isInteger()) return nil[cur++].getInteger();
        return this->next();
    }

    bool hasNext() {
        if (curUnfolded < unfolded.size()) return true;
        else if (cur < nil.size()) {
            if (nil[cur].isInteger()) return true;
            unfolded = unfold(nil[cur++].getList());
            curUnfolded = 0;
            return this->hasNext();
        }
        return false;
    }
};
```

##### 310. Minimum Height Trees
The first idea (naive one) is to use dfs from each root and get the maximum depth for each root. Do it more smartly and keep track of the depth from one node to another, so the algorithm does less work. Technically, each edge is only traversed twice.

```cpp
vector<int> findMinHeightTrees(int n, vector<pair<int, int>>& edges) {
    unordered_map<int, vector<pair<int, int>>> graph; // nodeA -> nodeB, minHeight
    vector<int> nodes(n, 0);
    for (pair<int, int> edge : edges) {
        graph[edge.first].push_back(pair<int, int> (edge.second, INT_MAX));
        graph[edge.second].push_back(pair<int, int> (edge.first, INT_MAX));
    }

    int minH = INT_MAX;
    vector<int> minHRoots;
    for (int node = 0; node < n; node++) {
        int height = dfsHeight(node, nodes, graph);
        if (height < minH) {
            minH = height;
            minHRoots.clear();
            minHRoots.push_back(node);
        } else if (height == minH) minHRoots.push_back(node);
    }
    return minHRoots;
}
int dfsHeight(int node, vector<int>& nodes, unordered_map<int, vector<pair<int, int>>>& graph) {
    nodes[node] = 1;
    int maxHeight = 0;
    for (int i = 0; i < graph[node].size(); i++) {
        if (nodes[graph[node][i].first]) continue;
        if (graph[node][i].second < INT_MAX) maxHeight = max(maxHeight, graph[node][i].second);
        else {
            int height = dfsHeight(graph[node][i].first, nodes, graph) + 1;
            graph[node][i].second = height;
            maxHeight = max(maxHeight, height);
        }
    }
    nodes[node] = 0;
    return maxHeight;
}
```

A better solution is to reduce the graph by trimming the leaves (nodes with only one or no inNode). Trim the graph repeatedly till there are more leaves than center nodes (or equal amount). Since each leave reduces the inDegree by 1, this indicates that all the nodes left can produce trees of the same height. This is a better solution. The idea of trimming is very useful in graph.

```cpp
vector<int> findMinHeightTrees(int n, vector<pair<int, int>>& edges) {
    vector<int> influx(n , 0);
    unordered_map<int, vector<int>> graph;
    for (pair<int, int> edge : edges) {
        graph[edge.first].push_back(edge.second);
        influx[edge.second]++;
        graph[edge.second].push_back(edge.first);
        influx[edge.first]++;
    }

    int nodeNum = n;
    vector<int> leaves;
    for (int i = 0; i < influx.size(); i++) {
        if (influx[i] <= 1) leaves.push_back(i);
    }
    while (nodeNum > leaves.size()) {
        nodeNum -= leaves.size();
        vector<int> newLeaves;
        for (int leave : leaves) {
            for (int inNode : graph[leave]) {
                if(--influx[inNode] == 1) newLeaves.push_back(inNode);
            }
        }
        leaves.swap(newLeaves);
    }
    return leaves;
}
```

##### 386. Lexicographical Numbers
I didn't really do it myself. The key is to find the pattern and then populate the vector with the o(1) procedure. An implementation from online discussion:

```cpp
vector<int> lexicalOrder(int n) {
    vector<int> res(n);
    int cur = 1;
    for (int i = 0; i < n; i++) {
        res[i] = cur;
        if (cur * 10 <= n) {
            cur *= 10;
        } else {
            if (cur >= n)
                cur /= 10;
            cur += 1;
            while (cur % 10 == 0)
                cur /= 10;
        }
    }
    return res;
}
```

##### 5. Longest Palindromic Substring
I didn't go fancy or anything with this one, just test each letter and see if it can become the "center" of the palindrome. Possible optimization is to start the process from the middle and then move to the sides (bisectionally or linearly). Stop when the palindrome size is greater than possible palindrome size. This can speed up for some cases such as "aaaaaaa" but it requires much more work to get the details right.

```cpp
string longestPalindrome(string s) {
    string ret = "";
    for (int i = 0; i < s.size(); i++) {
        string tmp = getPalindrome(i, s);
        if (tmp.size() > ret.size()) ret = tmp;
    }
    return ret;
}
string getPalindrome(int i, string& s) {
    string ret = "";
    int d = 0;
    while (i - d > -1 && i + d < s.size() && s[i - d] == s[i + d]) {
        d++;
    }
    ret = s.substr(i - d + 1, 2 * d - 1);
    d = 0;
    while (i - d > -1 && i + d + 1 < s.size() && s[i - d] == s[i + d + 1]) {
        d++;
    }
    if (2 * d > ret.size()) ret = s.substr(i - d + 1, 2 * d );
    return ret;
}
```

##### 332. Reconstruct Itinerary
Try to find a route first. Go back when reaching the end without using up all the tickets. Then keep doing this till an itinerary is found. Backtracking idea comes from [online](https://discuss.leetcode.com/topic/46577/28ms-c-beat-100-short-and-elegant).

```cpp
vector<string> findItinerary(vector<pair<string, string>> tickets) {
    unordered_map<string, priority_queue<string, vector<string>, greater<string>>> ticketDict;
    int nPath = 0;
    for (pair<string, string> ticket : tickets) {
        ticketDict[ticket.first].push(ticket.second);
        nPath++;
    }

    stack<string> backTrack;
    vector<string> itinerary = {"JFK"};
    string dept = itinerary.back();
    while (nPath) {
        while (ticketDict[dept].empty()) {
            backTrack.push(dept);
            itinerary.pop_back();
            dept = itinerary.back();
        }
        while (ticketDict.find(dept) != ticketDict.end() && !ticketDict[dept].empty()) {
            itinerary.push_back(ticketDict[dept].top());
            ticketDict[dept].pop();
            dept = itinerary.back();
            nPath--;
        }
    }

    while (!backTrack.empty()) {
        itinerary.push_back(backTrack.top());
        backTrack.pop();
    }

    return itinerary;
}
```

##### 372. Super Pow

The key is to figure out the math formula for `mod`. Suppose we have `x0 % NUM = x1` and `y0 % NUM = y1`, then we will have the following relationship

```
(x0 * y0) % NUM = (x1 * y1) % NUM
```

This is clear if we divide a number into `a = a1 + a2` where `a1 % NUM = 0` and `a2 = a % NUM`. I'll leave the rest of math, but by multiplying the numbers out, one can easily prove the above relationship.

With this concept in mind, this problem is simplified to finding out the residue at each level and keep working out the "large" array `b`, whose size really doesn't matter that much at this stage. The complexity is `o(n)` where `n` is the size of `b`.

```cpp
const int NUM = 1337;
int superPow(int a, vector<int>& b) {
    if (b.empty()) return 1;
    int res = 1;
    int lastDigRes = a % NUM;
    for (int i = b.size() - 1; i > -1; i--) {
        int powTo = b[i];
        res *= myPow(lastDigRes, powTo);
        if (res >= NUM) res %= NUM;
        if (res == 0) return 0;
        lastDigRes = myPow(lastDigRes, 10);
    }
    return res;
}
int myPow(int a, int b) {
    int tmp = 1;
    for (int i = 0; i < b; i++) {
        tmp *= a;
        if (tmp >= NUM) tmp %= NUM;
    }
    return tmp;
}
```

##### 142. Linked List Cycle II

Use two runner pointers at different speed. Once they meet, return one to the start and have them keep going at the same pace. Eventually they will meet at the start of the cycle. Very nice insight into this kind of problems.

```cpp
ListNode *detectCycle(ListNode *head) {
    if (head == NULL) return NULL;
    ListNode *sNode = head, *dNode = head;

    while (dNode != NULL) {
        dNode = dNode->next;
        if (dNode != NULL && dNode->next != NULL) dNode = dNode->next;
        else return NULL;
        sNode = sNode->next;
        if (dNode == sNode) break;
    }
    dNode = head;
    while (sNode != dNode) {
        dNode = dNode->next;
        sNode = sNode->next;
    }
    return dNode;
}
```

##### 322. Coin Change

(Was asked about this question for 3 times at least and I still didn't know the dp solution. Fail.) Well, do it using DP, look for previous best change and see if you can do better.

```cpp
int coinChange(vector<int>& coins, int amount) {
    vector<int> dpArray(amount + 1, amount + 1);
    dpArray[0] = 0;
    for (int i = 0; i < dpArray.size(); i++) {
        for (int coin: coins) {
            if (i - coin >= 0) {
                dpArray[i] = min(dpArray[i], dpArray[i - coin] + 1);
            }
        }
    }

    return dpArray.back() > amount ? -1 : dpArray.back();
}
```
##### 131. Palindrome Partitioning

This one is related to 132. The key is to make a matrix that keeps track of all the palindroms using start and end indices. When you have that matrix, the rest is fairly simple. I used a dfs to traverse through the matrix and get all the possible outcomes out. Something else may perform better.

```cpp
int minCut(string s) {
    int L = s.size();
    bool palMatrix[L][L];
    for (int i = 0; i < L; i++) palMatrix[i][i] = true;
    for (int i = 0; i < L - 1; i++) palMatrix[i + 1][i] = (s[i + 1] == s[i]);
    for (int j = 2; j < L; j++) {
        for (int i = 0; i < L - j; i++) {
            if(s[i] == s[i + j]) {
                palMatrix[i + j][i] = palMatrix[i + j - 1][i + 1];
            } else palMatrix[i + j][i] = 0;
        }
    }

    int dpArray[L];
    for (int i = 0; i < L; i++) {
        if (palMatrix[i][0] != 0) {
            dpArray[i] = 0;
        } else {
            dpArray[i] = INT_MAX;
            for (int j = 0; j < i; j++) {
                if (palMatrix[i][j + 1]) {
                    dpArray[i] = min(dpArray[i], dpArray[j] + 1);
                }
            }
        }
    }
    return dpArray[L-1];
}
```

##### 132. Palindrome Partitioning II

Well, DP. There are two keys to this question. First, you need to construct this matrix to reduce the complexity of checking every possible palindrome o(n^3) to o(n^2) in this case. Then use a DP array to see how many steps do you need to jump from start to the end (recall the stair jump problem), this costs o(n^2) worst.

```cpp
int minCut(string s) {
    int L = s.size();
    bool palMatrix[L][L];
    for (int i = 0; i < L; i++) palMatrix[i][i] = true;
    for (int i = 0; i < L - 1; i++) palMatrix[i + 1][i] = (s[i + 1] == s[i]);
    for (int j = 2; j < L; j++) {
        for (int i = 0; i < L - j; i++) {
            if(s[i] == s[i + j]) {
                palMatrix[i + j][i] = palMatrix[i + j - 1][i + 1];
            } else palMatrix[i + j][i] = 0;
        }
    }

    int dpArray[L];
    for (int i = 0; i < L; i++) {
        if (palMatrix[i][0] != 0) {
            dpArray[i] = 0;
        } else {
            dpArray[i] = INT_MAX;
            for (int j = 0; j < i; j++) {
                if (palMatrix[i][j + 1]) {
                    dpArray[i] = min(dpArray[i], dpArray[j] + 1);
                }
            }
        }
    }
    return dpArray[L-1];
}
```

##### 416. Partition Equal Subset Sum

Remember to think in term of DP if you're stuck. One key is to realize that if the sum is odd, there is no way a partition can work. Then if it is even, you only need to see if you can sum up to the even number with all the numbers given. This is where the DP comes in: for every number in the DP array, check if you can use some number in the given set to jump from a smaller number in the DP array.

A proper translation of this algorithm:

```cpp
bool canPartition(vector<int>& nums) {
    int sum = 0;
    for (int i = 0; i < nums.size(); i++) sum += nums[i];
    if (sum & 1) return false;

    int halfSize = sum / 2;
    vector<bool> dpArray(halfSize + 1, false);

    dpArray[0] = true;
    for (int num : nums) {
        for (int i = halfSize; i >= num; i--) {
            if (dpArray[i - num]) dpArray[i] = true;
        }
    }
    return dpArray[halfSize];
}
```

A performance one that uses `bitset` to optimize the space usage.

```cpp
bool canPartition(vector<int>& nums) {
    const int MAX_NUM = 100;
    const int MAX_ARRAY_SIZE = 200;
    bitset<MAX_NUM * MAX_ARRAY_SIZE / 2 + 1> bits(1);
    int sum = 0;
    for (auto n : nums) {
        sum += n;
        bits |= bits << n;
    }
    return !(sum % 2) && bits[sum / 2];
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

Implementation using doubly-linked list. Don't see too much a performance boost here. Some online solution does not manage the memory leak (by not calling `delete`) and gets a speed boost :<. Perhaps a singly linked list can do the job better but I'm not sure how to keep track of the tail. Perhaps reverse the last link and take a node? IDK.

```cpp
struct Node {
    Node *prev, *next;
    int val;
    Node(int x) : val(x), next(NULL) {};
};

class LRUCache {
public:
    LRUCache(int capacity) {
        cap = capacity;
        size = 0;
        head = tail = NULL;
    }
    int get(int key) {
        if (cache.find(key) == cache.end()) return -1;
        move_to_front(cache[key].first);
        return cache[key].second;
    }
    void set(int key, int value) {
        if (cache.find(key) == cache.end()) {
            Node *node = new Node(key);
            cache[key] = make_pair(node, value);
            if (size++ == 0) tail = node;
            else head->prev = node;
            node->next = head;
            head = node;
            if (size > cap) {
                cache.erase(tail->val);
                tail = tail->prev;
                delete tail->next;
                tail->next = NULL;
            }
        } else {
            Node *node = cache[key].first;
            move_to_front(node);
            cache[key].second = value;
        }
    }
    void move_to_front(Node *node) {
        if (node != head) {
            if (node == tail) {
                tail = tail->prev;
                if (tail != NULL) tail->next = NULL;
                if (node->prev != NULL) node->prev->next = NULL;
            }

            // Remove from the list
            if (node->prev != NULL) node->prev->next = node->next;
            if (node->next != NULL) node->next->prev = node->prev;

            // Move to the head
            node->prev = NULL;
            node->next = head;
            head->prev = node;
            head = node;
        }
    }
private:
    int size, cap;
    Node *head, *tail;
    unordered_map<int, pair<Node*, int> > cache;
};
```

##### 174. Dungeon Game
Dynamic programming to keep track of maximum health needed. It took me a while because I was starting from the beginning, but apparently back tracking is more appropriate in this case. I implemented the code after reviewing some discussions online.

```cpp
int calculateMinimumHP(vector<vector<int>>& dungeon) {
    if (dungeon.empty() || dungeon[0].empty()) return 1;
    int M = dungeon.size();
    int N = dungeon[0].size();
    for (int i = M - 1; i > -1; i--) {
        for (int j = N - 1; j > -1; j--) {
            int tmp = INT_MAX;
            if (i < M - 1) tmp = min(tmp, dungeon[i + 1][j]);
            if (j < N - 1) tmp = min(tmp, dungeon[i][j + 1]);
            dungeon[i][j] = max(1, (tmp == INT_MAX ? 1 : tmp) - dungeon[i][j]);
        }
    }
    return dungeon[0][0];
}
```

##### 44. Wildcard Matching (*)
Iterative algorithm from [online discussion](https://discuss.leetcode.com/topic/21577/my-three-c-solutions-iterative-16ms-dp-180ms-modified-recursion-88ms/2). Whenever a '*' wildcard is encountered, mark the position and backtrack if necessary, otherwise keep going till things break.

```cpp
bool isMatch(string s, string p) {
    int iLast = -1, jLast = -1, i, j;
    for (i = 0, j = 0; i < s.size(); i++, j++) {
        if (p[j] == '*') {
            iLast = i--;
            jLast = j;
        } else {
            if (p[j] != '?' && p[j] != s[i]) {
                if (jLast < 0) return false;
                i = iLast++;
                j = jLast;
            }
        }
    }
    while (j < p.size() && (p[j] == '*')) j++;
    return j == p.size();
}
```

##### 287. Find the Duplicate Number

This problem has a lot of easier variations but the imposed conditions make the whole problem much harder. For easier approach, one can

1. Sort the array and find the duplicate easily. `o(nlog(n))` and you have to be able to change the array, but super easy to implement.
2. Sum the elements up and use math formula to find the missing number. However, this does not work for this one because there can be more than one duplicates.
3. Use a map to keep track of existing elements. Nice and simple but needs extra space.

Last but not least, see the array as a linked list (because all indices are in the range of the array itself). Then we know that if there are duplicates of one particular, unique number, then as we traverse the linked list, we're bound to come back to one of the elements here.

So my implementation did not really keep the array "unchanged", but it is easy to fix - have the number set to be negative of itself instead of `0` and in the end negate those numbers back in one giant sweep. The algorithm will run `o(n)`.

```cpp
int findDuplicate(vector<int>& nums) {
    if (nums.empty()) return -1;
    int index = 0;
    while (nums[index]) {
        int tmp = nums[index];
        nums[index] = 0;
        index = tmp;
    }
    return index;
}
```
