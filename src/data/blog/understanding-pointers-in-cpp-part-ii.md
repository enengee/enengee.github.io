---
title: "Understanding Pointers in C++: Part II"
pubDatetime: 2018-08-18T10:15:00.000Z
tags:
  - cpp
---

Excerpt from [Linus Torvalds's](https://en.wikipedia.org/wiki/Linus_Torvalds) answer in a [Slashdot interview](http://meta.slashdot.org/story/12/10/11/0030249/linus-torvalds-answers-your-questions):

> I've seen too many people who delete a singly-linked list entry by keeping track of the "prev" entry, and then to delete the entry, doing something like:
>
> if (prev)
>   prev->next = entry->next;
> else
>   head = entry->next;
>
> and whenever I see code like that, I just go "This person doesn't understand pointers". And it's sadly quite common. People who understand pointers just use a "pointer to the entry pointer", and initialize that with the address of the list_head. And then as they traverse the list, they can remove the entry without using any conditionals, by just doing:
>
> *pp = entry->next;

In this post, we will explore the solution proposed by Linus. First, let's look at the function to delete a node in a singly linked list as most people would typically write it:

```cpp
// Delete `target` node from a singly linked list whose head is `head`.
void deleteNode(ListNode*& head, ListNode* target) {
  ListNode* entry = head;
  ListNode* prev = NULL;

  while(entry) {
    if (entry == target) {
      if (prev) prev->next = entry->next;
      else head = entry->next;
      break;
    }

    prev = entry;
    entry = entry->next;
  }
	
  delete target;
}
```

A bit of explanation about passing `head` by reference: if the `head` parameter is not passed by reference, we would only be able to delete nodes that are not the head (because the statement `entry = entry->next` for the first time—i.e., `entry = head->next`—allows `entry` to traverse the pointers allocated on the **HEAP**). We wouldn't be able to handle the case where the head itself is being deleted, because in that case, the `head` pointer inside the function and the one outside are completely different. If `target == head`, the statement `head = target->next` would run. First, this only changes the `head` pointer inside the function (the `head` pointer outside the function remains unaffected). Second, it only changes where this internal `head` pointer points (to the memory at `target->next`), rather than actually modifying the pointer on the **HEAP** that the original `head` pointer points to. In summary, we pass `head` by reference so that any changes to `head` inside the function are reflected outside the function.

The above approach is not optimal because to delete a node, we need to know its preceding node. Since the `head` does not have a preceding node, this special case must always be handled. Linus Torvalds wants to avoid writing extra code for this special case by using a pointer-to-pointer (double pointer) to identify the "preceding" pointer for every node, including the `head`. To understand this, first, consider that if a singly linked list has n nodes, these nodes reside on the **HEAP** (at n memory locations). Each node contains a `next` pointer that points to the next node's memory. So, which pointer points to the first node? That's `head`! And it resides on the **STACK**:

<figure>
  <img
    src="/images/pointer_3.jpg"
    alt="Figure 1. Illustration of memory at the beginning."
  />
    <figcaption class="text-center">
    Figure 1. Illustration of memory at the beginning.
  </figcaption>
</figure>

First, initialize the `entry` pointer to point to the first node of the list:

```cpp
ListNode* entry = head;
```

Nodes in the linked list are traversed by `entry`, similar to the first algorithm, and at any point, we need to know the pointer that points to the current node. When `entry` points to the first node, the `head` pointer on the **STACK** can be viewed as the pointer "preceding" the first node. Naturally, we need a pointer to this `head` pointer—a pointer-to-pointer (double pointer):

```cpp
ListNode** pp = &head;
```

Illustration of memory at this point:

<figure>
  <img
    src="/images/pointer_4.jpg"
    alt="Figure 2. Illustration of memory with `entry` and `pp`."
  />
    <figcaption class="text-center">
    Figure 2. Illustration of memory with entry and pp.
  </figcaption>
</figure>

Now, we no longer need to worry about the special case where the head node is deleted, as we have identified a pointer pointing to every node (even the first one). The rest of the logic is similar to the first algorithm. Here is the full code for the new approach:

```cpp
// Delete `target` node from a singly linked list whose head is `head`.
void deleteNode(ListNode*& head, ListNode* target) {
  ListNode** pp = &head;
  ListNode* entry = head;

  while(entry) {
    if (entry == target) {
      *pp = entry->next;
      break;
    }
    pp = &(entry->next);
    entry = entry->next;
  }
  delete target;
}
```

And we can even do it without using `entry`:

```cpp
// Delete `target` node from a singly linked list whose head is `head`.
void deleteNode(ListNode*& head, ListNode* target) {
  ListNode** pp = &head;
  while(*pp != target) {
    pp = &((*pp)->next);
  }
  *pp = target->next;
  delete target;
}
```
