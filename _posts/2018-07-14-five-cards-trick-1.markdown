---
layout: post
title:  Five Cards Trick - 1
date:   2018-07-12 
permalink: /fivecardstrick-1
author: "Alok Bakshi"
---

> Real magic refers to the magic that is not real, while the magic that is real, that can actually be done, is not real magic. --  Daniel Dennett

## Introduction

Magic in most of the tricks is due to the sleight of hand but the beauty of the "five cards trick" written below  is that performing it needs nothing more than the mental calculation.

The trick is performed as follows:

<span style="color:blue">
Alice and Bob are two magicians with a deck of 52 standard cards with them. Alice comes to you and ask you to pick any *five* cards. She carefully looks at your choice and then hands you back one card out of those five. Thereafter she takes the remaining four cards and give those to the Bob.</span>

<span style="color:blue">
Note that it's only Alice's prerogative to choose the handed over card. Moreover Bob is standing away and no information is passed to him with the exception of *ordered* list of remaining four cards.</span>

<span style="color:blue">
Thereafter Bob does some mental calculation -- while chanting abracadabra simultaneously -- and correctly figures out the fifth card, which you have safely kept hidden away from his prying eye.
</span>

## Problem Reformulation

Before discussing the solution (you can see it [here](https://puzzling.stackexchange.com/questions/6569/a-five-card-trick-how-does-it-work) let us first rephrase the problem in mathematical terms. 

There is an one-to-one correspondence between deck of fifty two cards and set of natural numbers between 0 and 51 (endpoints included). For example, we may number cards of Club suit between 0 and 12,cards of Diamond suit between 13 and 25, and so on. For definiteness, we can take the below map to make the correspondence between cards and numbers 

$$
\begin{align*}
\textbf{Suits}: \ \  &\mbox{Heart} \longleftrightarrow 0, \ \ \mbox{Diamond} \longleftrightarrow 1, \ \ \mbox{Club} \longleftrightarrow 2, \ \ \mbox{Spade} \longleftrightarrow 3 \\
\textbf{Face}: \ \ &\mbox{Jack} \longleftrightarrow 11, \ \ \mbox{Queen} \longleftrightarrow 12, \ \ \mbox{King} \longleftrightarrow 0, \ \ \mbox{Ace $\ldots$ Ten} \longleftrightarrow 1 \ldots 10 
\end{align*}
$$

$$
\mbox{Card (Suits: S, Face: F)} \longleftrightarrow 13 * S + F
$$



Getting back to the problem, in terms of natural numbers, it can be rephrased as follows:

<span style="color:blue">Given five distinct numbers $$ 0 \leq u, v, x, y, z \leq 51 $$, find a strategy of choosing $$ u $$ such that by looking at the remaining numbers presented in some order, say $$ y, z, x, v $$ one can figure out the value of $$ u $$.</span>

## Possible Solution Strategies

Before looking at the solution and refining it thereafter, let us first try to see if the naive approach can lead us somewhere.

One can immediately see that remaining four numbers can be arranged in $$ 4! = 24 $$ different ways. On the other hand, there are 48 distinct possibilities for the fifth number (as four out of fifty two numbers are already known). Thus one needs to hide that particular number, whose number of possibilities stay within twenty four.

As an example, one might simply choose to hide the median $$ x_3 $$ out of the ordered five numbers $$  0 \leq x_1 < x_2 < x_3 < x_4 < x_5 \leq 51 $$. Thus with the remaining ordered four numbers $$  0 \leq x_1 < x_2 < x_4 < x_5 \leq 51 $$, one can specify $$ x_3 $$ from the permutations of remaining four only if $$ \mid x_4 - x_2 \mid \leq 25 $$. So we see that this naive approach is not foolproof. Similarly one can try other *similar* strategies (say, always hide the extreme number) but those strategies will not succeed in every possible situation.

Thus relative ordering of the numbers does not provide enough information and we need to incorporate their magnitudes into our calculation as well. 

## An Elegant Solution (based upon Pigeonhole Principle) 

Having (hopefully) realized the difficulty of problem, let us look at one of the elegant solution, which is an application of [Pigeonhole principle](https://en.wikipedia.org/wiki/Pigeonhole_principle). 

To apply it, let us partition the collection of numbers into four equal sized sets, namely:

* $$ A = \{n \in \mathbb{N} \ | \ 0 \leq n \leq 12 \} $$
* $$ B = \{n \in \mathbb{N} \ | \ 13 \leq n \leq 25 \} $$
* $$ C = \{n \in \mathbb{N} \ | \ 26 \leq n \leq 38 \} $$
* $$ D = \{n \in \mathbb{N} \ | \ 39 \leq n \leq 51 \} $$

then out of the five numbers, two of them will definitely fall into the same partition, which for the sake of definiteness we take as $$ B $$.

Thus suppose that $$ x, y, z, u, v $$ are the five distinct numbers with $$  u, v \in B $$ and therefore $$ \mid u - v \mid \leq \mid B \mid = 13 $$. In that case we can choose to hide either of $$ u $$ or $$ v $$ and put the other on top (or other previously specified location) of the returned list of numbers. Thus we can immediately narrow down our search to the list of twelve numbers (as  $$ \mid u - v \mid \leq 13 $$ and $$ u, v $$ are distinct). 

Having already fixed the position of one in the returned list of four numbers, we can rearrange the remaining numbers in $$ 3! = 6 $$ distinct ways. It is impossible to represent twelve numbers out of these six distinct cases. 

But if we choose the hidden number (out of the two candidates $$ u $$ and $$ v $$) cleverly then we can narrow our search further down from twelve to six. To that end, we equip the set $$ B $$ with the modular arithmetic operation

$$
x \oplus y := \ \ 13 + \left(\left( x + y \right) \bmod 13\right)
$$

(i.e. mentally picture it as an 13 hour clock where digits run between 13 and 25) then either $$ u $$ lies within six units right (or clockwise) to $$ v $$ or $$ v $$ lies within six units right to $$ u $$. Thus by hiding the appropriate number, we can make sure that it is within six units right to the topmost number of the returned list of four numbers. Furthermore the actual offset can then be conveniently represented by the permutation of the remaining three numbers. 

For concreteness, the offset ($$ 1 \leq \mathrm{offset} \leq 6 $$) can be read from the ordered returned list of remaining three numbers $$ \{x, y, z \} $$ as follows:

* $$ x < y < z \qquad \longleftrightarrow \qquad \mathrm{offset} = 1 $$
* $$ x < z < y \qquad \longleftrightarrow \qquad \mathrm{offset} = 2 $$
* $$ y < x < z \qquad \longleftrightarrow \qquad \mathrm{offset} = 3 $$
* $$ y < z < x \qquad \longleftrightarrow \qquad \mathrm{offset} = 4 $$
* $$ z < x < y \qquad \longleftrightarrow \qquad \mathrm{offset} = 5 $$
* $$ z < y < x \qquad \longleftrightarrow \qquad \mathrm{offset} = 6 $$

## An Illustrative Example

Suppose that Alice is presented with $$ \heartsuit 3, \ \diamondsuit 9, \ \ \clubsuit K, \ \  \clubsuit 8, \ \ \spadesuit 5 $$. In terms of the numbers, these are 3, 22, 26, 34, and 44 respectively. 

Thereafter Alice will notice that numbers 26 and 34 belong to the same set $$ C $$ defined above. Moreover the number 26 is at a distance of 5 to the right of 34 because under the map $$ x \mapsto x \oplus 1 = 26 + \left((x + 1) \bmod 13 \right)$$

$$ 
34 \rightarrow 35 \rightarrow 36 \rightarrow 37 \rightarrow 38 \rightarrow 26
$$

Also she would note that 34 is at a distance of 8 units to the right of 26, that's why she had to go the other way around.

Therefore she will hide the number 26 and put 34 on top of the returned list of four numbers. Now she also need to encode the offset 5 in terms of the permutation of remaining three numbers (namely 3, 22, 44).  According to the list above it means, that she needs to put that in the order of (44, 3, 22). 

Thus she will arrange the remaining four cards as (34, 44, 3, 22) i.e. $$ \clubsuit 8, \ \spadesuit 5, \ \heartsuit 3, \ \diamondsuit 9$$ and give those to Bob. After receiving the ordered list of these four cards, Bob can immediately decode it to find the missing card namely $$ \clubsuit K $$ to (hopefully) the surprise of everyone else.

## Concluding Remark

We can in fact improve upon this method (explained [here](http://www.apprendre-en-ligne.net/crypto/magie/card.pdf), which will be the topic of the next post. Above procedure is implemented in `C++` language and you can find it [here](https://github.com/alokbakshi/Five-Cards-Trick).
