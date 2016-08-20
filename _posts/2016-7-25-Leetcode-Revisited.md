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
