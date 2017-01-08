---
title:  "Useful C++ Functions"
excerpt: "Some useful c++ functions that are not automatically supported"
categories:
  - Utility
tags:
  - CODE_DEBUG_LIFE
use_math: false
---

Split a string in C++.

```cpp
void split(const string &s, char delim, vector<string> &elems) {
    stringstream ss;
    ss.str(s);
    string item;
    while (getline(ss, item, delim)) {
        elems.push_back(item);
    }
}
```

Initialize an integer array with value

```cpp
int array[n];
memset(array, value, sizeof(array));
```

more concisely,

```cpp
int array[n] = {value};
```

Initialize a hashset

```cpp
const unordered_set<int> SET = {1, 2, 3, 4, 5};
```