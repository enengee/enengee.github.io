---
title: "Understanding Pointers in C++: Part I"
pubDatetime: 2018-07-20T13:48:00.000Z
tags:
  - cpp
---

Before diving into the problem, let's first define a "node" structure:

```cpp
struct ListNode {
  int value;
  ListNode* next;
  ListNode(int x): value(x), next(NULL) {}
};
```

With the above structure, we can create 3 nodes like this:

```cpp
ListNode* head = new ListNode(1);
ListNode* node2 = new ListNode(2);
ListNode* node3 = new ListNode(3);
```

Let's explain the meaning of the above assignment statements in more detail:

- The `new ListNode(1)` operator allocates memory on the **HEAP** and returns the address of this memory region.
- `ListNode* head`: declares a pointer variable that points to the `ListNode` data type; this pointer variable is stored on the **STACK**.
- The assignment `ListNode* head = new ListNode(1)`: assigns a memory address to a pointer. An assignment involving a pointer usually has a pointer on the left side and a memory address $X$ on the right side. Thus, the assignment can be understood as: **the pointer `head` points to the memory location at address $X$, which stores `ListNode(1)`.**

Illustration:

<figure>
  <img
    src="/images/pointer_1.jpg"
    alt="Figure 1. How nodes are allocated in memory."
  />
    <figcaption class="text-center">
    Figure 1. How nodes are allocated in memory.
  </figcaption>
</figure>

Next, link these 3 nodes together to create a singly linked list:

```cpp
head->next = node2;
node2->next = node3;
```

The above assignments are explained in a completely similar way (you will notice that essentially, this operation is the same as the allocation above):

- `head` is a pointer variable on the **STACK** that points to memory on the **HEAP** of type `ListNode` containing `value=1` and `next=NULL`. Thus, `head->next` is the `next` pointer variable within that `ListNode` on the **HEAP**.
- The command `head->next = node2` has a pointer on its left side and the address of the memory on the **HEAP** that `node2` is pointing to on its right side (`value=2` and `next=NULL`). As analyzed above, this assignment makes the `head->next` pointer point to the memory location at the address of `node2`.

Analyzing the remaining command similarly, we have the following illustration:

<figure>
  <img
    src="/images/pointer_2.jpg"
    alt="Figure 2. How nodes link together to form a singly linked list."
  />
    <figcaption class="text-center">
    Figure 2. How nodes link together to form a singly linked list.
  </figcaption>
</figure>
