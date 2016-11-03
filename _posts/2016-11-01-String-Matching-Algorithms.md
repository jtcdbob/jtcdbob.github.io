---
title:  "String matching algorithms"
excerpt: "Study notes on string matching algorithms (Boyer-moore, KMP and Rabin Karp)."
categories:
  - Blog
tags:
  - CODE_DEBUG_LIFE
use_math: false
---

### Introduction

There are three popular string matching algorithms that show up constantly and I have been procrastinating to study them for a long time. Finally I did and here are some of the information I kept:

A basic overview of the string matching/searching problems - [Wiki page](https://en.wikipedia.org/wiki/String_searching_algorithm).

The problem basically simplifies to the following

* Give two strings `text` and `pattern` (assuming `text.size() > pattern.size()`).
* Find the indices in `text` where the substrings match `pattern` completely
* The string can consist of any legal characters.

A naive implementation of the problem is straightforward: you go through each position in `text` and do a linear matching with `pattern`. This approach is not horrible (~o(m(n-m))) but in some cases can be extremely slow, so we would like to speed things up a bit.

There are three popular fast algorithms:

1. Rabin-Karp
2. Knuth-Morris-Pratt (KMP)
3. Boyer-Moore

### Rabin-Karp

The core idea behind Rabin-Karp is to use a hash to store a string combination, and each time you do not have to compare the substring with pattern but instead compare the hash first and a linear comparison if necessary.

The hash is design such that a substring `text[i:j]` can be easily updated by `text[i]` and `text[j + 1]`. In other words, the following operation:

```
hash(text[i+1:j+1]) = rehash(hash(text[i:j]), text[i], text[j+1])
```

is cheap. This is done by a smart math formula:

```
hash(text[i+1:j+1]) = d * (hash(text[i:j]) – text[i] * h) + text[j+1]) mod q
```

where `d` is the number of characters in the alphabet, `q` is a good choice of prime number (supposedly big enough) and `h` is `d^(pattern.size()-1)`. This is essentially a smarter bit map thing for quick hashing and rehashing. The entire operation is relatively cheap too.

A few notes on Rabin-Karp:

* The comparison at each position is faster than naive version, but it still goes through each position. As we'll see later, this can be avoided.
* The average and best case runtime is o(n+m), but the worst time is o(nm) when all the characters in `text` and `pattern` are the same. So pretty bad worst case.

See this [post](http://www.geeksforgeeks.org/searching-for-patterns-set-3-rabin-karp-algorithm/) for more details and C++ code.

### KMP

For both naive and Rabin-Karp, each position in `text` is iterated through. Think of the Naive version, if a mismatch is found in the middle of pattern, the entire match operation is then discarded without acknowledging any of the work. KMP algorithm ([wiki page](https://en.wikipedia.org/wiki/Knuth–Morris–Pratt_algorithm) is essentially a strategy to reuse the portion in the `pattern` that matches and skip through the `text`.

KMP precomputes a table for the `pattern`, `lps` (longest proper prefix). The table identifies the repeating portion of the `pattern` and suggests a way to move forward faster.

Then in the string match process, when a mismatch happens, the matching start position no longer moves by `1` but by the amount indicated in `lps`. This way, the work done in previous matching session doesn't go to waste and the string traversal goes much faster.

Some notes:

* KMP algorithm works very well when there are a lot of repetitive portion in the pattern.
* The time complexity of KMP is o(n).

See this [post](http://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/) for more details and C++ code

### Boyer-moore

Boyer-moore([wiki page](https://en.wikipedia.org/wiki/Boyer–Moore_string_search_algorithm)) is the benchmark for string matching algorithms. It has the best average performance and its worst performance is the same as naive one (o(nm)).

Boyer-moore first align the `text` and `pattern`, then starts comparing them from the end (instead of begining as usual). Then when there is a mismatch, it applies two rules to determine how much the alignment shoud shift:

1. Bad character, also known as bad heuristics. When a character mismatch happens, look to the left of the pattern and find the first occurance of that character to make the new alignment.
2. Good suffix, also known as good heuristics. Alternatively, the alignment can move to a new position where the tail string matches the suffix of substring (kinda confusing description here, look it up).

The two rules work well individually but Boyer-moore combines them together and always choose the one that allows larger shift.

There is cost associated with building the table for good/bad heuristics. The algorithm works well in general and it is highly efficient especially when the `pattern` is much smaller than the `text`.

There are two videos discussing this algorithm in general: [part 1](https://www.youtube.com/watch?v=4Xyhb72LCX4), [part 2](https://www.youtube.com/watch?v=Wj606N0IAsw).
