---
title: Entry Software Engineer Mock Interview
draft: false
tags:
  - coding
  - interviews
date: 2024-06-16
---
 A family friend messaged me a few weeks ago since he was in the interview loop at a couple companies. He wanted to gain some exposure to the interview process, and given that the job market for entry-level positions is pretty tough right now, I wanted to help. He shared a job description with me, and it mostly seemed related to systems stuff, so I tried to tailor my questions towards that. Here's what I asked, and why.

## Topical Questions
I broke this section up into 4 areas. These were meant to get more info about what the candidate knows about the topics mentioned in the job description:
1. OS/Systems
2. Scheduling/Kernel
3. Memory Allocation
4. Threads and Processes

### OS/Systems
> What are the differences between monolithic architectures and microservice
architectures?

#### Why I Asked This
Distributed systems are very core to current technological stacks, especially for companies that are at large scale. In the resources I've gone through, like college classes, books, etc. usually, the authors discuss how computing started, and where it is now. Picture the software class that you learned about [Moore's Law](https://en.wikipedia.org/wiki/Moore%27s_law) in. This question is open enough that the interviewer and interviewee can have a decent discussion about the topics at hand. *Even if the interviewee doesn't know about the terms exactly, they might be able to hold a decent conversation and reason through.* 

#### What I Look For
- What is a monolithic architecture?
- What is a microservice architecture?
- When would you pick a microservice architecture? (Short answer: At scale)
- When would you pick a monolithic architecture, and why? (Short answer: When scale isn't as important. Calls over network can be time-costly!)

### Scheduling/Kernel
> What is process scheduling and why is it important?

#### Why I Asked This
Scheduling is core to why our personal machines are able to compute as much as they can and as quickly as they do. As a developer, I think understanding process scheduling is a good first step to concurrent code (think event loops). This topic is core to operating systems, which was also a part of the job description.

#### What I Look For
- At a high level, what is the kernel? (Short answer: A part of the OS managing resources and comms between hardware and software)
- What are some different options for scheduling and what are the benefits/consequences?

### Memory Allocation
> What are memory leaks and how are they introduced? What should be done to
ensure that they don't creep in? Do you know of any tools that can be used to
debug mem leaks?

#### Why I Asked This
Again, memory leaks are one of those core concepts that luckily have mostly been abstracted from us nowadays. Having an understanding of what they are, how they can happen, and how to debug them are things that are often asked in classes and a good opportunity for interviewees to share extras on what they know about this topic.

#### What I Look For
- Do you know some of the common sources of memory problems? (Short answer: buffer overflow, allocation without freeing, etc.)
- What are the general solutions to the above sources?
- Do you know what Valgrind is and how it's used? AKA, did you pay attention in class?

### Threads and Processes
> What are the differences between processes and threads?

#### Why I Asked This
Honestly, pretty similar to above. This one's a classic textbook problem and I vaguely remember in one of our exams in college we had a problem similar to the above. It's another good way to show off what you know. I also asked this question to get a bit more insights into whether or not I should ask the last question I had for the interviewee for the leetcode portion.

#### What I Look For
- Do you know what's in the TCB vs PCB? (Short answer: PCB can contain multiple threads, threads cannot have multiple processes, but there's a lot more)
- When would you use processes over threads? (Short answer: Core parallelism, Isolation, if you use python no GIL, etc.)
- When would you use threads over processes? (Short answer: Threads can share memory, they're way more lightweight, etc.)

## LeetCode Questions
I started off with a no-BS question and then made an easier version of it to be part 1 and an enhancement to be part 3. The original question then took the part 2 slot. So this ended up being a 3 part question, which I hope was interesting to the interviewee.

### Part 1: Find In BST
Given a Binary Search Tree, find and return the node that matches the value being searched for.
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* findInBST(TreeNode* root, int val) {
        // Your implementation here
    }
};
```


### Part 2: Find in Tree
Now, instead of a binary search tree, you just have a tree structure. Find and return the node that matches the value being searched for.
```c++
/**
 * Definition for a tree node.
 * struct TreeNode {
 *     int val;
 *     std::vector<TreeNode*> children;
 *     TreeNode() : val(0), children(std::vector<TreeNode*>()) {}
 *     TreeNode(int x) : val(x), children(std::vector<TreeNode*>()) {}
 *     TreeNode(int x, std::vector<TreeNode*> children) : val(x), children(children) {}
 * };
 */
class Solution {
public:
    TreeNode* findInTree(TreeNode* root, int val) {
        // Your implementation here
    }
};
```

### Part 3: Multithreading fun!
How would you introduce multithreading to the above Part 2? 

**Hint**: Imagine you had the following:
- a fixed number T threads at your disposal
- a function that can validate if the value is found in a list of nodes
- a function that can get children of a node
- a task queue
