---
title: "Book Review: Test-Driven Java Development by Viktor Farcic and Alex Garcia (2015)"
pubDatetime: 2018-07-01T08:25:00.000Z
tags:
  - book review
  - testing
  - java
  - tdd
---

[Link to the book](https://www.packtpub.com/application-development/test-driven-java-development).

It's been a while since I last read a book from [PacktPub](https://www.packtpub.com); as expected, the book is very easy to learn from and highly practical. Unlike the book [Test-Driven Development By Example](/review-sach-test-driven-development-by-example), even those who know nothing about TDD can read this one.

Overall, the content of the book is divided into 3 main parts:
- First, the authors introduce TDD as well as unit testing.
- The middle chapters, each introducing and practicing with a library that supports TDD and unit testing (JUnit 4, Mockito, etc.).
- The end of the book contains the authors' shared best practices in TDD.

If you follow the instructions in the book closely, you will get a general overview of TDD, how to use libraries, and many opportunities to practice the **test/compile/run/refactor** cycle. Although for each library, the authors provide an example (a small project) to practice it, readers only reach a basic level of usage and don't have the chance to dive deep into the libraries. Therefore, I evaluate the content of the book as having more breadth than depth, and I also find that the examples provided by the authors in this book are not as good or as subtle as those in [Test-Driven Development By Example](/_posts/2018-05-30-review-sach-test-driven-development-by-example.md).

To summarize, I learned a pretty interesting trick, which is how to name a test method using the 3 keywords _Given_, _When_, and _Then_, similar to BDD. Some excerpts from the book that I particularly like:

> **Speed is the key**: Imagine a game of ping pong (or table tennis). The game is very fast; sometimes it is hard to even follow the ball when professionals play the game. TDD is very similar. TDD veterans tend not to spend more than a minute on either side of the table (test and implementation). Write a short test and run all tests (ping), write the implementation and run all tests (pong), write another test (ping), write implementation of that test (pong), refactor and confirm that all tests are passing (score), and then repeat—ping, pong, ping, pong, ping, pong, score, serve again. Do not try to make the perfect code. Instead, try to keep the ball rolling until you think that the time is right to score (refactor).

> **It's not about testing**: T in TDD is often misunderstood. Test-driven development is the way we approach the design. It is the way to force us to think about the implementation and to what the code needs to do before writing it. It is the way to focus on requirements and implementation of just one thing at a time—organize your thoughts and better structure the code. This does not mean that tests resulting from TDD are useless—it is far from that. They are very useful and they allow us to develop with great speed without being afraid that something will be broken. This is especially true when refactoring takes place. Being able to reorganize the code while having the confidence that no functionality is broken is a huge boost to the quality.

> Requirements (specifications and user stories) are written before the code that implements them. They come first so they define the code, not the other way around. The same can be said for tests. If they are written after the code is done, in a certain way, that code (and the functionalities it implements) is defining tests. Tests that are defined by an already existing application are biased. They have a tendency to confirm what code does, and not to test whether client's expectations are met, or that the code is behaving as expected.

> A test must not only fail, but must fail for the expected reason.

> **Red Green Refactor process**
> - Write a test, this test must fail (for some specific requirement or reason), we're in red.
> - Run all tests and confirm the last one fails, red
> - Write the code to pass the test, red
> - Run all tests. green
> - Refactor (optional), it's not mandatory to run this step at the end of each cycle.
> - Repeat

> **Benefit of writing test first**
> - Code coverage
> - Focus on requirements

> What is the difference in the way we write unit tests in the context of TDD? The major differentiator is in when.

> TDD benefit: giving executable documentation that is always up to date.

> Legacy code is code without test.

Additionally, Chapter 10 has some quite good best practices that I haven't mentioned above.

Rating: **3/5**.
