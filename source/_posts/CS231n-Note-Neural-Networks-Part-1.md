---
title: '[CS231n Note] Neural Networks Part 1'
date: 2016-11-13 20:11:02
tags:
categories: Neural Networks
---
![](/images/Note-CS231n-Neural-Networks-Part-1-f1.png)
<!-- more -->
## Commonly used activation functions
**Sigmoid**. It has two major drawbacks:
- Sigmoids saturate and kill gradients. when the neuron’s activation saturates at either tail of 0 or 1, the gradient at these regions is almost zero. If the local gradient is very small, it will effectively “kill” the gradient and almost no signal will flow through the neuron to its weights and recursively to its data.
- Sigmoid outputs are not zero-centered. If the data coming into a neuron is always positive (e.g. $x>0$ elementwise in $f=w^Tx+b$)), then the gradient on the weights $w$ will during backpropagation become either all be positive, or all negative. This could introduce undesirable zig-zagging dynamics in the gradient updates for the weights.

**Tanh**. Like the sigmoid neuron, its activations saturate, but unlike the sigmoid neuron its output is zero-centered.

**ReLU**. The Rectified Linear Unit has become very popular in the last few years.
- (+) It was found to greatly accelerate the convergence of stochastic gradient descent compared to the sigmoid/tanh functions. 
- (+) The ReLU can be implemented by simply thresholding a matrix of activations at zero.
- (-) ReLU units can “die”. If the unit is inactive in forward pass, then its local gradient is zero in backward pass. As a result, the unit will forever be zero.

**Leaky ReLU**. Leaky ReLUs are one attempt to fix the “dying ReLU” problem. Instead of the function being zero when $x < 0$, a leaky ReLU will instead have a small negative slope. That is, the function computes $f(x)=𝟙(x<0)(αx)+𝟙(x>=0)(x)$.

**Maxout**. The Maxout neuron computes the function $max(w^{T_1}x+b1,w^{T_2}x+b2)$. Notice that both ReLU and Leaky ReLU are a special case of this form.

**TLDR**. “What neuron type should I use?” Use the ReLU non-linearity, be careful with your learning rates and possibly monitor the fraction of “dead” units in a network. If this concerns you, give Leaky ReLU or Maxout a try. Never use sigmoid. Try tanh, but expect it to work worse than ReLU/Maxout.

## Neural Network architectures

**Naming conventions**. Notice that when we say N-layer neural network, we do not count the input layer. 

**Output layer**. Unlike all layers in a Neural Network, the output layer neurons most commonly do not have an activation function. This is because the last output layer is usually taken to represent the class scores.

## Representational power
It turns out that Neural Networks with at least one hidden layer are universal approximators. In other words, the neural network can approximate any continuous function. The fact that deeper networks (with multiple hidden layers) can work better than a single-hidden-layer networks is an empirical observation, despite the fact that their representational power is equal.

## Setting number of layers and their sizes
In practice, it is always better to use these methods to control overfitting instead of the number of neurons. There are many ways to prevent overfitting in Neural Networks (such as L2 regularization, dropout, input noise). 

The subtle reason behind this is that smaller networks are harder to train with local methods such as Gradient Descent: It’s clear that their loss functions have relatively few local minima, but it turns out that many of these minima are easier to converge to, and that they are bad (i.e. with high loss). Conversely, bigger neural networks contain significantly more local minima, but these minima turn out to be much better in terms of their actual loss. 


