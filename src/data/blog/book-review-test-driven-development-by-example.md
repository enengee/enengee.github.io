---
title: "Book Review: Test-Driven Development: By Example by Kent Beck (2002)"
pubDatetime: 2018-05-28T13:07:00.000Z
tags:
  - book review
  - testing
  - tdd
---

[Link to the book](https://www.amazon.com/Test-Driven-Development-Kent-Beck/dp/0321146530).

I don't remember exactly how I found out about this book, but I sought it out when I needed to learn about [Test-Driven Development](https://en.wikipedia.org/wiki/Test-driven_development) (TDD) to prepare for a junior interview.

The tone of the book is not very formal; the author writes as if he were talking directly to the reader. To read this book effectively, you should have a basic understanding of TDD and unit testing (no need to go deep, just getting the general concept is fine), and know how to use JUnit (basics). There are many reference sources available online.

The book mainly consists of 3 main chapters:

- **Chapter 1**: The author guides you through practicing TDD with JUnit (I recommend using Eclipse) by building a program called Money. In my opinion, this is the best chapter of the book: you will grasp how the **test/compile/run/refactor** process works, how this process supports and guides the program's source code, and the way the author leads ideas through testing and object-oriented principles is very subtle. This example also helped me answer some initial questions like: Should I have multiple `assert` calls in one test? or How should I group tests? etc.

- **Chapter 2**: The author guides you through implementing and testing a unit test framework (using Python, but the language isn't the main point here), helping readers better understand the ideas behind concepts like `test`, `setUp`, `tearDown`, `testSuite`, etc.

- **Chapter 3**: This chapter discusses patterns in TDD, where the author primarily shares experiences and discusses the correct approach to TDD: design principles for test cases, some code refactoring techniques, etc. This chapter can be quite dry because it lacks examples and the vocabulary is somewhat difficult; however, the author also points out some elements that I find important, specifically: tests must be independent of each other (_"If I had one test broken, I wanted one problem. If I had two tests broken, I wanted two problems"_), and independent in terms of execution order (executing test A first should not affect the result of test B executed afterward, and vice-versa).

Rating: **3/5**. Beginners should focus on Chapter 1, 2, and the beginning of Chapter 3.
