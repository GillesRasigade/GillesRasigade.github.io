---
layout: page
title: Collatz conjecture
categories:
  - maths
  - colltatz conjecture
  - syracuse conjecture
date: 2018-05-15
---

This very first article [^1] is interesting.

The following formula is obtained by applying $$n$$ times the reverse function $$f$$ to a number $$a \in \mathbb{N}$$:

$$
f^{-n}(a) = \frac{1}{3^n} \left( a 2^{\sum\limits_{i=0}^n p_i} - \sum\limits_{i=1}^n 3^{i-1} 2^{\sum\limits_{j=i+1}^n} p_j \right)
$$

<!--
$$
b_{a}^{p} = \frac{1}{3^p}(b_{a}^{0}\times2^{\sum_{i=0}^{p}n_{i}}-\sum_{i=0}^{p} 3^
{p-i}\times2^{\sum_{j=1}^{i-1}n_{j}})
$$
-->

## The problem


$$
f(n) =
\begin{cases}
n/2 & \text{if }n \equiv 0 \mod 2 \\
3n+1 & \text{if }n \equiv 1 \mod 2
\end{cases}
$$

The conjecture

> This process will eventually reach the number 1, regardless of which positive integer is chosen initially.

## Generator

Any function of the form:


$$
\begin{aligned}
\mathcal{G} :\ & \mathbb{N} \rightarrow \mathbb{N} \\
& a \rightarrow a \times 2^p ,p \in \mathbb{N}
\end{aligned}
$$


is defined as a generator for the Syracuse problem because any number leading to a function of this form will fall down to $$1$$ after $$n$$ iterations.

Anytime a number $$a$$ is having the following property, the conjecture is demonstrated:


$$
\exists p \in \mathbb{N}, f(a) = 3a + 1 = \mathcal{G}(p)
$$


This means that any number respecting the following equation is validating the conjecture:


$$
a = \frac{\mathcal{G}(p) - 1}{3} = \frac{2^p - 1}{3}
$$


The question is then: is there for any number $$a \in \mathbb{N}$$, a fixed number of iteration for $$f$$ leading to a generator function?

If this is the case, the conjecture is demonstrated.

### Relation between generators

> A _generator_ has **several** _children_ but a **single** _parent_.

Is the following relation truth?


$$
\forall b \in \mathbb{N}, \exists! a \in \mathbb{N} / f(\mathcal{G}_b) = \mathcal{G}_a
$$


Demonstration

`Written, must be copied here`

Conclusion

A _generator_ has several children by the application of the function $$f$$ but has a single parent by the application of the same function.

### Neutral element

The _generator_ $$\mathcal{G}_1$$ is a neutral element for the function $$f$$:


$$
f(\mathcal{G}_1) = \mathcal{G}_1
$$


with


$$
\mathcal{G}_1 = 2^p, p \in \mathbb{N}
$$


Questions:

* Do we have other neutral elements for the function $$f$$?
* Is there a relation between neutral elements and cycles for the function $$f$$?

#### Demonstration


$$
\begin{aligned}
f(\mathcal{G}_a) & = & \mathcal{G}_a & \in \mathbb{N}\\
3 \times a 2^p + 1 & = & a 2^q & => q > p\\
a \left( 2^q - 3 \times 2^p \right) & = & 1\\
a 2^p \left( 2^{q-p} - 3 \right) & = & 1\\
a & = & \frac{1}{2^p \left( 2^{q-p} - 3 \right)}\\
a, p, n \in \mathbb{N} & => & a = 1 &
\end{aligned}
$$


### Children of a generator

A generator $$\mathcal{G}_a$$ is having the following children by application of the reverse function of $$f$$:


$$
\begin{aligned}
f^{-1}(\mathcal{G}_a) & = & \frac{a 2^p - 1}{3} \in \mathbb{N}, p \in \mathbb{N} \\
\end{aligned}
$$


What are the values of $$p$$?

<!--
| $$n$$ | $$2^n$$ | $$1$$ |$$3$$ | $$5$$ | $$7$$ | $$9$$ | $$11$$ | $$13$$ | $$15$$ | $$17$$ | $$19$$ |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| $$0$$ | $$1$$ |||||||||||
-->

All odd numbers can be defined with the following form:

$$
a = 3 \left( n \pm 0,2 \right), n \in \mathbb{N^*}
$$

Leading to

$$
1, 3, 5 - 7, 9, 11 - 13, 15, 17 - 19, 21, 23 - 25, 27, 29 - ...
$$

Thus, what are accepted values of $$p$$ with the following form?

$$
\begin{aligned}
f^{-1}(\mathcal{G}_a) & = & \frac{a 2^p - 1}{3} & \in \mathbb{N}, p \in \mathbb{N} \\
& = & \frac{3 \left( n \pm 0,2 \right) 2^p - 1}{3} & \in\mathbb{N}, \forall n \in \mathbb{N}
\end{aligned}
$$

For $$a = 3n, n \in \mathbb{N}$$

$$
\begin{aligned}
f^{-1}(\mathcal{G}_a) & = & \frac{a 2^p - 1}{3} & \in \mathbb{N}, p \in \mathbb{N} \\
& = & \frac{3 n 2^p - 1}{3} & \in \mathbb{N}, \forall n \in \mathbb{N} \\
& = & n2^p - \frac{1}{3} & \notin \mathbb{N}, \forall n, p \in \mathbb{N}
\end{aligned}
$$

> **Conclusion** A generator of type $$\mathcal{G}_{3k}, k \in \mathbb{N}$$ does not have any children generator.

We can **thus** simplify the problem. What are values of $$p$$ for $$a = 3 \left( n \pm 2 \right), n \in \mathbb{N}$$ leading to:

$$
\frac{a 2^p - 1}{3} \in \mathbb{N}
$$

For $$a = 3n - 2, n \in \mathbb{N}$$

$$
\begin{aligned}
f^{-1}(\mathcal{G}_a) & = & \frac{a 2^p - 1}{3} & \in \mathbb{N}, p \in \mathbb{N} \\
& = & \frac{3 n 2^p - 2^{p+1} - 1}{3} \\
& = & n2^p - \frac{2^{p+1} + 1}{3} & \in \mathbb{N} \text{ if } p+1 \equiv 2k + 1, k \in \mathbb{N} \\
\end{aligned}
$$

> **Conclusion** For $$a = 3n - 2, n \in \mathbb{N}$$, only values of $$p$$ of the form $$p = 2k, k \in \mathbb{N}$$ are defining valid children generators for$$\mathcal{G}_a$$.

For $$a = 3n + 2, n \in \mathbb{N}$$

$$
\begin{aligned}
f^{-1}(\mathcal{G}_a) & = & \frac{a 2^p - 1}{3} & \in \mathbb{N}, p \in \mathbb{N} \\
& = & \frac{3 n 2^p + 2^{p+1} - 1}{3} \\
& = & n2^p + \frac{2^{p+1} - 1}{3} & \in \mathbb{N} \text{ if } p+1 \equiv 2k, k \in \mathbb{N} \\
\end{aligned}
$$

> **Conclusion** For $$a = 3n + 2, n \in \mathbb{N}$$, only values of $$p$$ of the form $$p = 2k + 1, k \in \mathbb{N}$$ are defining valid children generators for $$\mathcal{G}_a$$.

Based on previous results, we can build the following array

| $$n$$ | $$2^n$$ | $$1$$ | $$5$$ | $$7$$ | $$11$$ | $$13$$ | $$17$$ | $$19$$ | $$23$$ | $$25$$ | $$29$$ | $$31$$ |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| $$0$$ | $$1$$ |$$0$$||$$2$$||$$4$$||$$6$$||$$8$$||$$10$$|
| $$1$$ | $$2$$ ||$$3$$||$$7$$||$$11$$||$$15$$||$$19$$||
| $$2$$ | $$4$$ |$$1$$||$$9$$||$$17$$||$$25$$||$$33$$||$$41$$|
| $$3$$ | $$8$$ ||$$13$$||$$29$$||$$45$$||$$61$$||$$...$$||
| $$4$$ | $$16$$ |$$5$$||$$37$$||$$69$$||$$101$$||$$...$$||$$...$$|
| $$5$$ | $$32$$ ||$$53$$||$$117$$||$$181$$||$$...$$||||
| $$6$$ | $$64$$ |$$21$$||$$149$$||$$277$$||$$405$$||$$...$$|||
| $$7$$ | $$128$$ ||$$213$$||$$469$$||$$725$$||$$...$$||||
| $$8$$ | $$256$$ |$$85$$||$$597$$||$$1109$$||$$1621$$||$$...$$|||
| $$9$$ | $$512$$ ||$$853$$||$$1877$$||$$2901$$||$$...$$||||
| $$10$$ | $$1024$$ |$$341$$||$$2389$$||$$4437$$||$$6485$$||$$...$$|||
| $$11$$ | $$2048$$ ||$$...$$||$$...$$||$$...$$||$$...$$||||
| $$12$$ | $$4096$$ |$$1365$$||$$...$$||$$...$$||$$...$$|||||

Is there a relation between generators values for consecutive valid odd numbers for a given $$n$$ value?

$$
\begin{aligned}
\delta^n_\leftrightarrow & = & \frac{\left( b + 6 \right) 2^n - 1}{3} - \frac{b 2^n - 1}{3} \\
& = & \frac{6 \times 2^n}{3} \\
& = & 2 \times 2^2 \\
\delta^n_\leftrightarrow & = & 2^{n+1}
\end{aligned}
$$

> **Conclusion** In the array given above, the difference between 2 values on the same row is $$2^{n+1}, n \in \mathbb{N} $$.

Is there a relation between generators values for consecutive values power of $$2$$ for a given $$a$$ value?

$$
\begin{aligned}
\delta^n_{a, \updownarrow} & = & \frac{a 2^{n+2} - 1}{3} - \frac{a 2^n - 1}{3} \\
& = & \frac{a 2^n \left( 2^2 - 1 \right) - 1}{3} \\
& = & \frac{3 a 2^n}{3} \\
\delta^n_{a, \updownarrow} & = & a 2^n
\end{aligned}
$$

<!--
Can two different generators $$\mathcal{G}_b$$ and $$\mathcal{G}_c$$ have the same parent?

$$
\begin{aligned}
\mathcal{G}_a & = & f( \mathcal{G}_b ) & = & f( \mathcal{G}_c ) \\
& & 3 b 2^p +1 & = & 3 c 2^q + 1 \\
& & b 2^p & = & c 2^q \\
& & b & = & c 2^{q-p}
\end{aligned}
$$

> **Conclusion** In both situation where $$q > p$$ or $$p > q$$, we have $$b \in \mathcal{G}_c$$ or $$c \in \mathcal{G}_b$$ leading to the conclusion than $$b = c$$.
-->

### $$\mathbb{N}$$ mapped

Do we have an equivalence between each $$n \in \mathbb{N}$$?

If we are observiing the arra accurately, we can extract that if any number of $$\mathbb{N}$$ can be expressed with:

$$
n = \frac{2^{2p} \left( 1 + 6q \right) - 1}{3} \text{ where } p, q \in \mathbb{N}
$$

or

$$
n = \frac{2^{2p + 1} \left( 5 + 6q \right) - 1}{3} \text{ where } p, q \in \mathbb{N}
$$

### Order relation between generators

The following order between generators can be easily extracted from the array:

$$
1, 5, 13, 17, 11, 7, 37, 49, 65, 43, 229, 305, 203, 541, 721, 961, 5125, 6833, 4555, 6073, 32389, ...
$$

Understanding

$$
\mathcal{G}_1 \supset \mathcal{G}_5 \supset \mathcal{G}_{13} \supset ...
$$

or

$$
\begin{aligned}
f(\mathcal{G}_5) = \mathcal{G}_1 \\
f^2(\mathcal{G}_{13}) = \mathcal{G}_1 \\
f^3(\mathcal{G}_{17} = \mathcal{G}_1 \\
...
\end{aligned}
$$

---

[^1] [Wikipedia](https://en.wikipedia.org/wiki/Collatz_conjecture)
