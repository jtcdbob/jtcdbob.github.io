---
title:  Notes on C++ STL
excerpt: "Some review notes for C++ STL"
categories:
  - Blog
tags:
  - CODE_DEBUG_LIFE
---
I always want a more organized way to review C++ STL containers before my interview, so here it goes [for C++11]:

----------


## Common member functions

### Iterators:

* `begin(), end(), rbegin(), rend()` - return (reverse) first/last iterator.
* `cbegin(), cend(), crbegin(), crend()` - constant iterator, can't change the value it points to.

### Capacity function:
* `empty()` - true if the size is 0; false otherwise.
* `size()` - return size.
* `max_size()` - maximum size the container can hold (due to memory limit). Usually a good check when resizing.




-------------
## Useful Containers:

**list** - *doubly linked list*. Constant insertion/deletion and iterate in both directions. Also good for moving elements around when iterators are already obtained. However, access to an element takes o(n) time.

* `front()` - first element
* `back()` - last element
* `push_front()`
* `pop_front()`
* `push_back()`
* `pop_back()`
* `insert(iterator, [number], element)`
* `insert(iterator, first, last)` - copy everything between first - last and then insert them before iterator. e.g. `l.insert(l.begin(), vec.begin(), vec.end())`;
* `erase(position) / erase(first, last)`
* `remove(val)`;
* `remove_if(is_condition())`; [a bool function] o(n)
* `sort([comparator])`; ~o(NlogN)
* `unique(is_condition())`;
* `merge(list secondList, comparator)`; remove all in second and insert into first by order

**map** - implemented as *binary search tree*. key values are used to uniquely identify the elements. A strict order is preserved in the map (can use an iterator to go through it).

`map<key, value, [comparator]>`

`operator[]`

`insert([iterator], pair<,>)`: provide an iterator as a hint position for maximum efficiency insertion.

`erase(key)/erase(iterator)`;

`clear()`; clear all contents

`find(key)`; return iterator for specific key. `map.end()` if not found. o(logN)

`lower_bound(key)/upper_bound(key)`: return iterator for lower/upper bound on map[key]. o(logN).

**multimap** - similar to map, except one key can map to several values. Likely a binary search tree with a linked list in its value. Notice that now find() will return the first iterator. Values in each bucket are sorted by insertion order (nothing you can do about it. Avoid this container all together if sorting the value is important to you.)

**queue** - use deque as underlying structure if no container class is specified. FIFO.

`queue<dataType, [container class]>`

`front()`

`back()`

`pop()`

`push()`

**priority_queue** - use vector as underlying structure if no container class is specified. Similar to heap. Implemented as containers adaptor(not sure what it means, just remember it as heap and know how to implement using array).

`priority_queue<dataType, [container class, comparator]>`; the last two are optional but usually used.

`top()`; o(1)

`push()`; (push_heap is called) for array heap implementation, it should be o(logN)

`pop()` (pop_heap() and pop_back() each) similarly,o(logN).

**set** - *binary search trees*. Basically a tree without mapping here.

`set<dataType, comparator>`

`insert()`

`find(val)`

**multiset** - again, multimap without mapping

**stack** - use deque as underlying structure if no container class is specified. FILO.

`top()`

`push()`

`pop()`

**unordered_map** - hash map. Not quite interested in detailed implementation. Basically hash to a bucket and in the bucket there is a linked list. Rehash when the linked list gets too long. One can specify hash and comparator if wanted (not going there for now).

`operator[]`

`insert();`

`erase();`

`clear();`

`bucket_count()`; how many buckets the hashmap has

`max_bucket_count()`; how many buckets the hashmap can have

`bucket_size()`;

`bucket()`; locate an element's bucket

`load_factor()`; `max_load_factor()`;

`rehash(n)`;  force rehash

`reserve(n)`; set the container to most appropriate to contain at least n



**unordered_multimap** - one key can have multiple duplicate values that are grouped in one bucket. One can use equal_range to iterate through them.

`equal_range()`: return a pair that keeps the first and last iterator to one range.

Neat example:
{% highlight ruby %}
auto range = myumm.equal_range("strawberry");
  for_each (
    range.first,
    range.second,
    [](stringmap::value_type& x){std::cout << " " << x.second;}
  );
{% endhighlight %}

**unordered_set**: again, unordered_map without mapping

**unordered_multiset**: no mapping.

**vector**: use dynamically allocated arrays for storage (continuous memory!). Vector will reallocate itself in order to grow in size. Efficient in access element. Not so much when inserting/deleting in the middle.

`resize(n)`;

`capacity()`;

`reserve`;

`shrink_to_fit()`

`push_back(val)`;

`pop_back()`;

`insert(iterator, [number], val)`; insert before the iterator

`insert(iterator, first, last)`

**forward_list** - probably not useful at this moment. It's basically singly linked list. The data insertion and deletion efficiency is its top concern, even at the price of high access cost. For sparse data (sparse matrices, graphs) that cannot fit into one memory/cache, maybe it is preferred to use forward_list rather than containers such as vector. [It is only somewhat smaller and more efficient than list]

HashMap: when a linked list gets too long, the hashmap will just double its size and rehash to make sure the time complexity is still good.
