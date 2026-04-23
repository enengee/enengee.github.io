---
title: "Logic of the Tortoise and Hare algorithm"
pubDatetime: 2018-05-03T19:32:00.000Z
tags:
  - algorithm
---

I'm quite busy right now writing my graduation report and finishing up various projects, so this post will be written in a bit of a "freestyle" manner. Who cares, anyway?

Given a singly linked list, the problem is to check whether it contains a cycle. If it does, we need to find the starting element of the cycle $\mu$ and the cycle's length $\lambda$.

<figure>
  <img
    src="/images/cycle_linked_list.jpg"
    alt="Figure 1. A singly linked list with μ = x2 and λ = 5"
  />
    <figcaption class="text-center">
    Figure 1. A singly linked list with μ = x_2 and λ = 5
  </figcaption>
</figure>

Implicitly, this means $x_7 = x_2, x_8 = x_3, \dots$ and so on.

It is important to note that $\mu$ does not exist if $x_6$ "loops back" to the head of the linked list $x_0$; there must be some initial elements before the cycle begins (like $x_0, x_1$ in this case).

The Tortoise and Hare algorithm is named after its mechanism: two pointers, representing a tortoise and a hare, start from the same point. The hare moves faster than the tortoise: for every step the tortoise takes, the hare takes $s$ steps ($s > 1$).

Suppose both pointers start from some $x_i$. After the tortoise takes $j$ steps and stops at $x_{i+j}$, the hare will have taken $sj$ steps and stopped at $x_{i+sj}$.

If the linked list does not have a cycle, the hare pointer will eventually reach `NULL`.

If there is a cycle, we expect the two pointers to eventually meet at some element (which must be a part of the cycle).

Suppose they meet after $j$ steps, meaning $x_{i+j} = x_{i+sj}$.

This occurs when $x_{i+j}$ and $x_{i+sj}$ are separated by an integer multiple of the cycle length $\lambda$:

$$ (i+sj) - (i+j) = k\lambda \\ $$
$$ j = \frac{k\lambda}{s-1} $$

It is easy to see that for $s = 2$, the equation is always satisfied for some $j, k, \lambda$.

In other words: **If the tortoise and the hare start at the same point, and the hare moves two steps for every one step the tortoise takes, they are guaranteed to meet after a finite number of steps.**

Now, let's find $\mu$. To visualize this, with $s=2$ and assuming both start at $x_0$, they would meet at $x_5$.

At this point, the tortoise is at $x_{i+j} = x_{i+k\lambda}$ (which is $x_5$). We then reset the hare to the starting position $x_i$ (which is $x_0$). _(Note: $x_i$ must be outside the cycle to find $\mu$)_.

$x_i$ and $x_{i+k\lambda}$ are separated by an integer multiple of the cycle length. However, $x_i \neq x_{i+k\lambda}$ because one belongs to the cycle and the other does not. By moving both pointers one step at a time, we maintain the $k\lambda$ distance. As soon as the hare pointer enters the cycle, it will meet the tortoise exactly at the cycle's starting element, $\mu$.

Back to our example: the hare is at $x_0$, and the tortoise is at $x_5$. Both then move to $x_1$ and $x_6$, respectively. After one more step, they meet at $x_2$. Thus, $x_2$ is the starting point of the cycle.

Finding $\lambda$ is straightforward: since we've identified the starting element, we can simply move one pointer around the cycle and count the steps until it returns to $\mu$.

Here is the C++ code (it doesn't handle the case where there is no cycle; I'll leave that as an exercise for the reader):

```cpp
void detectCycle(Node * x0) {
  Node * tho = x0, * rua = x0;
  do {
    rua = rua->next;
    tho = tho->next->next;
  } while(rua != tho);

  // Find mu
  rua = x0; // Reset one pointer to start
  while(rua != tho) {
    rua = rua->next;
    tho = tho->next;
  }
  // Now rua (or tho) is mu

  // Find lambda
  int lambda = 0;
  do {
    lambda++;
    tho = tho->next;
  } while(tho != rua);
}
```
