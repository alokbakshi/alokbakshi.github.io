---
layout: post
title:  Hoeffding Lemma
date:   2019-06-02 
permalink: /hoeffding-1
author: "Alok Bakshi"
---

## Introduction
We recall the *Markov's inequality*: Given a non--negative random variable \\(X\\) with finite expected value, one has the following probability estimate

$$
\displaystyle \mathbb{P}(X \geq t) \ \leq \ \dfrac{\mathbb{E}(X)}{t}.
$$

For a more general case of any random variable \\(X\\) with finite expcted value \\(\mathbb{E}(X)\\) and variance \\( \mathrm{Var}(X)\\), Markov's inequality on \\( \left(X - \mathbb{E}(X) \right)^2 \\) yields

$$
\displaystyle \mathbb{P}\left( \left| X - \mathbb{E}(X) \right| \geq t \right) \ \leq \ \dfrac{\mathrm{Var(X)}}{t^2}
$$

One of the application of above could be to bound the probability estimate that mean does deviate much from the average. For instance, if $$ \left\{ X_i \right\}_{i=1}^n $$ are independent identically distributed random variables with $$ \mathbb{E}(X_i) = \mu \mbox{ and } \mathrm{Var}(X_i) = \sigma^2 $$ then the Chebyshev's inequality implies the following

$$
\displaystyle \mathbb{P}\left( \left| \bar{X} - \mu \right| \geq t \right) \ \leq \ \dfrac{\sigma^2}{n t^2}
$$

We notice that $$\bar{X} = \mu + \mathcal{O}\left( \frac{1}{n} \right)$$ and the goal of above article is to introduce other inequalities -- with additional hypothesis -- so that the error is of the order $$ \mathcal{O}(e^{ - C n^2 }) $$.

(to be continued ...)
