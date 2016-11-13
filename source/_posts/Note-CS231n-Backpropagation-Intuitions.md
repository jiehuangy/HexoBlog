---
title: 'Note CS231n Backpropagation, Intuitions'
date: 2016-11-13 16:02:05
tags:
categories:
---
{% img /images/Note-CS231n-Backpropagation-Intuitions-f1.png 650 %}
<!-- more -->

## Intuitive understanding of backpropagation
Every gate in a circuit diagram gets some inputs and can right away compute two things: 
1. its output value.
2. the local gradient of its inputs with respect to its output value.

During the backward pass in which the chain rule is applied recursively backwards through the circuit, the add gate learns that the gradient for its output was -4. If we anthropomorphize the circuit as wanting to output a higher value, then we can think of the circuit as “wanting” the output of the add gate to be lower (due to negative sign), and with a force of 4.

Backpropagation can thus be thought of as gates communicating to each other (through the gradient signal) whether they want their outputs to increase or decrease (and how strongly), so as to make the 

## Modularity: Sigmoid example
![](/images/Note-CS231n-Backpropagation-Intuitions-f2.png)
Example circuit for a 2D neuron with a sigmoid activation function. The inputs are [x0,x1] and the (learnable) weights of the neuron are [w0,w1,w2]. 
{% math %} 
\begin{aligned}
f(w,x)=\frac{1}{1+e^{-(w_{0}x_0+w_1x_1+w_2)}}
\end{aligned}
{% endmath %}

## Gradients add up at forks
If the forward expression involves the varibales multiple times, we mush be carefule to use `+=` to accumulate the gradient on these variables. This follows the multivariable chain rule in Calculus.

## Unintuitive effects and their consequences
if you multiplied all input data examples by 1000 during preprocessing, then the gradient on the weights will be 1000 times larger, and you’d have to lower the learning rate by that factor to compensate. This is why preprocessing matters a lot.


