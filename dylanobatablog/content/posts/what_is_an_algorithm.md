---
title: "What Exactly is an Algorithm?"
date: 2021-05-12T23:35:49-07:00
draft: false
---

Initially, I thought this post would be a simple introduction to algorithms and their analysis. Naturally, the first thing I thought to do was to introduce the definition of an algorithm. This is where I ran into some trouble. Typically in textbooks and online resources, an algorithm is informally introduced as a step-by-step process that solves a problem in a finite amount of time. We usually require algorithms to be unambiguous (each instruction to be executed has only one interpretation), and finite (they always come to an end). From there, authors usually introduce the notion of runtime analysis and Big O notation. I wasn't quite satisfied with this definition. I wanted and (expected) a rigorous mathematical definition for the term "algorithm", for which the entire field of computer science revolves around. As it turns out, there isn't a consensus definition for the term and researchers are looking to more precisely define it. Before looking at the evolution of the definition of "algorithm" and the arguments made for an absolute definition, I'll present a more formalized informal definition introduced by [Donald Knuth](https://en.wikipedia.org/wiki/Donald_Knuth).

**Definition**
: An ***algorithm*** is a finite set of rules that specify an ordered list of operations to follow to solve a certain type of problem. An algorithm has five properties that define it:
    1. Finiteness: An algorithm must always terminate in a finite amount of time.

    2. Definiteness: Each step of an algorithm must be precisely defined. Each action must be rigorously defined and unambiguously specified for each case.

    3. Input: An algorithm has zero or more input quantities to use, either at the beginning or throughout the computation process. 

    4. Output: An algorithm produces one or more output quantities which form a specified relation to the input quantities.

    5. Effectiveness: Each operation must be sufficiently basic so that they can be done exactly and finitely.

This definition seems to be good enough for most undergraduate analysis of algorithms textbooks to use and build on. A more layman definition would be a step by step guide to complete a certain task. Now back to our discussion. 

A good basis for formalizing the notion of an algorithm was introduced in the 1930's by Alonzo Church and Alan Turing with the [Church-Turing thesis](https://en.wikipedia.org/wiki/Church–Turing_thesis). Informally the thesis states that a function from natural numbers to natural numbers can be calculated by an effective procedure if and only if it is computable by a Turing machine. The two are generally credited with arriving at the same conclusion independently, however, their contributions did differ. Ultimately, Turing provided the mathematical specification for a computing machine. It was later proven that Church's lambda calculus, Turing's Turing machine, and Herbrand, Godel, and Kleene's recursive functions are all equivalent [models of computation](https://en.wikipedia.org/wiki/Model_of_computation). Here is the definition of a Turing machine.

**Definition**
: A **Turing machine** is a 7-tuple, \\( (Q, \Sigma, \Gamma, \delta, q_0, q_{accept}, q_{reject}) \\), where
\\( Q, \Sigma, \Gamma \\) are all finite sets and

    1. \\(Q\\) is the set of states,

    2. \\( \Sigma \\) is the input alphabet not containing the blank symbol ␣, 

    3. \\( \Gamma \\) is the tape alphabet, where ␣ \\( \in \Gamma \\) and \\(\Sigma \subseteq \Gamma\\) ,

    4. \\( \delta: Q \times \Gamma \rightarrow Q \times \Gamma \times \\{L, R\\} \\) is the transition function,

    5. \\(q_0 \in Q \\) is the start state,

    6. \\( q_{accept} \in Q \\) is the accept state, and

    7. \\( q_{reject} \in Q \\) is the reject state, where \\(q_{reject} \neq q_{accept} \\).

I should note that the \\(\delta\\) transition function is the most important part of this definition. It tells us how the machine gets from one step to the next, either by moving left(L) or right(R). With this, we are able to better formalize the notion of algorithm.

**Definition**
: An **algorithm** is a procedure that can be implemented by a Turing Machine.

This definition serves as a good basis for what an algorithm is but can be critiqued, which can be read [here](https://www.microsoft.com/en-us/research/wp-content/uploads/2017/01/164.pdf). In the 50's, [Kolmogorov](https://en.wikipedia.org/wiki/Andrey_Kolmogorov) introduced the notion of a [pointer machine](https://en.wikipedia.org/wiki/Pointer_machine), another model of computation, which perhaps didn't necessarily contribute to the narrowing of the definition, but did help in the analysis of time complexity for algorithms.

Why exactly is it so hard to find a formal definition for an algorithm? The computer scientist and mathematician [Yuri Gurevich](https://en.wikipedia.org/wiki/Yuri_Gurevich) compared the notion of algorithms to the notion of numbers. What exactly is a number? Like the term "algorithm", the term "number" does not have a formal definition. However, there are many classifications of numbers. For example, there are natural numbers, integers, rationals, reals, complex numbers, p-adic, etc. The notion of a number keeps expanding as we find more classifications for numbers that we **are** able to formally define. Likewise, we can classify and formally define classifications of algorithms. Some classifications of algorithms include sequential, parallel, quantum, interactive, etc. Dr. Gurevich has spent some time researching this topic and has axiomatically defined [sequential algorithms](https://web.eecs.umich.edu/~gurevich/Opera/141.pdf) and [parallel algorithms](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/tr-2006-137.pdf) using his [abstract state machine](https://www.microsoft.com/en-us/research/wp-content/uploads/2017/01/165.pdf) model of computation. As of now, there are classifications of algorithms that still need to be formally defined, but progress is being made. 


Further readings:

- [wiki/Algorithm](https://en.wikipedia.org/wiki/Algorithm#Computer_algorithms)

- [wiki/Algorithm Characterizations](https://en.wikipedia.org/wiki/Algorithm_characterizations)

- [Algorithms: A Quest for Absolute Definitions](https://www.microsoft.com/en-us/research/wp-content/uploads/2017/01/164.pdf) (Highly recommend)

- [What is an algorithm?](https://www.youtube.com/watch?v=I3MSDETx2a8&t=0s)

- [stackexchange/What exactly is an algorithm?](https://cs.stackexchange.com/questions/31932/what-exactly-is-an-algorithm)

- [Stanford/Church-Turing Thesis](https://plato.stanford.edu/entries/church-turing/)

- [Evolving Algebras](https://web.eecs.umich.edu/~gurevich/Opera/103.pdf)

- [stackexchange/Must an algorithm terminate?](https://math.stackexchange.com/questions/1561293/must-an-algorithm-terminate/1566254)

- [What exactly is a number?](https://math.stackexchange.com/questions/865409/what-exactly-is-a-number)

- [What are numbers? Part 1](https://www2.math.upenn.edu/~kirillov/MATH480-S08/WN1.pdf)

- [What are numbers? Part 2](https://www2.math.upenn.edu/~kirillov/MATH480-S08/WN2.pdf)
