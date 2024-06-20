---
title: DDIA -- Notes and Questions
draft: false
tags:
  - coding
  - dist-systems
date: 2024-06-19
---

# Designing Data Intensive Applications
[This book](https://dataintensive.net/)is considered the holy grail of app-building, especially at scale. I had started reading it a while ago, but didn't make it too far before I got busy with other things (a lame excuse). Starting again now and trying to write down some notes from my new starting point to the end. It's a really good intro to a bunch of different technologies and systems out there that exist to solve countless problems in the SWE space.

### SSTables + LSM Trees
- SSTable merging reminds me of [merge k sorted lists](https://leetcode.com/problems/merge-k-sorted-lists/description/)
- SSTables are very similar to hash tables
- To solve the problem of what to do when a crash happens -- it sounds like write ahead logging is generally the most common approach? These logs can be discareded when in-mem stuff is persisted to disk
- The indexing mechanism for Elasticsearch uses a term dict, in which a word is mapped to the IDs of all documents that contain that word
- Okay bloom filters come up here again and I've never really dug deep into them, but they've seemed really cool for a while:
	- A data struct that is able to tell you whether a queried value is "possibly in the set" or "definitely not in the set"
	- Basically, you have X hash functions. When you want to add something in, you apply all X hashes on the input and mark an array at the index that corresponds to the hash output as 1. When checking for existence, you run the input by all hash functions. If all return a 1, then that means the element may either exist or the combination of other values marked all those array positions as 1. If any one of the outputs is 0, you know for sure the element can't exist in the set since all values should be 1 if the element does exist.
	- This can solve the issue of querying for a key that doesn't exist in a more efficient manner.

### BTrees
- One of our projects in [CS186 at Berkeley](https://cs186berkeley.net/)was creating a B-Tree off of some starter code. Reading about these structures and thinking you understand them is easy, but implementing them definitely takes way more time and thought.
- They're like the epitome of organization and a really good implementation of trees -- each child reference narrows down the range of values you're searching for and the leaves contain your actual data values. 
- "A four-level tree of 4 KB pages with a branching factor of 500 can store up to 256TB"

### LSM Trees vs BTrees
- LSM trees are faster for writes while Btrees are faster for reads. LSM trees need to check several different data structures on read.
- Write amplification -> one presumed write turns into multiple due to underlying bookkeeping (repeated compaction for LSM Trees)
- LSM trees need compaction processes, which can happen at various times. Btrees are a bit more predictable
- Keys exist only at one place in the index for btrees but can have multiple copies in log systems. 

### Other indexing structures
- Clustered index = storing indexed rows directly within an index. Nonclustered index = storing only references to the data within the index
- Remember that indexing generally make writes more expensive -- they're not "free"
- Multi-dimensional indexes: imagine (latitude, longitude) being needed for spatial data.
- Fuzzy indexes allow for searching based on an edit-distance
- In-memory databases exist and grow bigger as the price difference between RAM and disk get lower and lower
- In mem databases gain performance benefits mainly from the fact that they don't need to incode in-mem data to a form that can be written to disk.