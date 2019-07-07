---
layout: post
title:  Assembly Lanugage on x86-64 for GNU/Linux with NASM
date:   2019-07-12 
permalink: /asm-1
author: "Alok Bakshi"
---



One of the simplest class of Mathematical optimization problems is *Linear Programs* (henceforth abbreviated as LP ) which find many [applications](https://en.wikipedia.org/wiki/Linear_programming#Uses) in modeling real world problems. In this post and the future ones, we will look at the naive procedure of solving a LP problem (A custom implementation of it is made [here](https://github.com/alokbakshi/Linear-Program-Solver)).


## Mathematical Formulation 

A Linear Program (LP) in standard form can be written as following:

$$

\begin{align*}

\mbox{Maximize  } z = z_0 + \sum_{i=1}^n c_i x_i \\

\mbox{subjected to the following constraints:} \\

\sum_{i = 1}^n a_{i j} x_i = b_j \ \ \ \forall 1 \leq j \leq m \\

x_i \geq 0 \ \ \ \forall 1 \leq i \leq n

\end{align*}

$$

In the above formulation, there are $$ n $$ variables and $$ m $$ constraints. We will declare $$ \mathbf{x} = \left(x_i\right)_{i=1}^n $$ to be a solution of above if it satisfies all of the above $$ m $$ constraints. An solution $$ \widetilde{\mathbf{x}} = \left(\widetilde{x_i}\right)_{i=1}^n $$ is called an optimal solution if for any other solution  $$ \mathbf{x}' = \left( x'_i \right)_{i=1}^n $$ we have

$$
\widetilde{z} = \widetilde{z_0} + \sum_{i=1}^n c_i \widetilde{x_i} \  \geq \ z' = z_0' + \sum_{i=1}^n c_i x'_i
$$

In case the optimal soliution exists we refer to $$ \widetilde{z} $$ as the optimal value. 

### Possible Scenarios

Given a LP problem in standard form, we could face the following

* LP has no solution. An example of it will be when the constraints contradict each other. For concreteness, the LP written below has no solution.

$$
\begin{align*}
\mbox{Maximize  } z &= x_1 + x_2 \\
x_1 + x_2 &\leq 2 \\
-x_1 - x_2 &\leq -4 \\
x_1 \geq 0&, \ x_2 \geq 0 \\
\end{align*}
$$

* Optimal value of the LP problem is infinite. For example, a LP problem written below has unbounded solution space and $$ z $$ can be made arbitrarily large 

$$
\begin{align*}
\mbox{Maximize  } z = 4 x_1 \\
- x_1 \leq - 2 \\
x_1 \geq 0
\end{align*}
$$


For clarity, we first make sure that none of the above two conditions arise. This can be ensured by making the following assumptions:

* $$ b_j \geq 0 $$ for all $$ j \in \left\{ 1, 2, \ldots, m\right\} $$. This ensures that there is at least one solution, namely $$ \mathbf{x} = (0, 0, \ldots, 0)$$.
* For all those variables $$ x_i : 1 \leq i \leq n$$ for which, $$ c_i \neq 0 $$ there exists a constraint $$ j : 1 \leq j \leq m $$ such that $$ a_{i j} \cdot c_i > 0 $$. It esnures that all of the variables $$ x_i $$ remain bounded and therefore so does the optimal value. 

Under these assumptions, there is an unique optimal value (and potentially several optimal solutions) of the above problem. [Simplex method](https://en.wikipedia.org/wiki/Simplex_algorithm) -- and variants thereof -- is one of the most popular algorithm to solve the above problem and in rest of the post we shall learn the basics behind this method.

