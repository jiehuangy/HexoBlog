---
title: '[CS231n Note] Neural Networks Part 2'
date: 2016-11-13 23:31:38
tags:
categories: Neural Networks
---
![](/images/CS231n-Note-Neural-Networks-Part-2-f1.png)
<!-- more -->

## Data Preprocessing
### Mean subtraction 
It involves subtracting the mean across every individual feature in the data, and has the geometric interpretation of centering the cloud of data around the origin along every dimension.


### Normalization 
It refers to normalizing the data dimensions so that they are of approximately the same scale. In case of images, the relative scales of pixels are already approximately equal (and in range from 0 to 255), so it is not strictly necessary to perform this additional preprocessing step.

### PCA and Whitening 
It is very often the case that you can get very good performance by training linear classifier on the PCA-reduced datasets, obtaining savings in both space and time. The **whitening** operation takes the data in the eigenbasis and divides every dimension by the eigenvalue to normalize the scale. The geometric interpretation of this transformation is that if the input data is a multivariable gaussian, then the whitened data will be a gaussian with zero mean and identity covariance matrix. One weakness of this transformation is that it can greatly exaggerate the noise in the data, since it stretches all dimensions (including the irrelevant dimensions of tiny variance that are mostly noise) to be of equal size in the input.

![](/images/CS231n-Note-Neural-Networks-Part-2-f2.png)

![](/images/CS231n-Note-Neural-Networks-Part-2-f3.png)

### In practice
We mention PCA/Whitening in these notes for completeness, but these transformations are not used with Convolutional Networks. However, it is very important to zero-center the data, and it is common to see normalization of every pixel as well.

## Weight Initialization
### Pitfall: all zero initialization
if every neuron in the network computes the same output, then they will also all compute the same gradients during backpropagation and undergo the exact same parameter updates. In other words, there is no source of asymmetry between neurons if their weights are initialized to be the same.

### Small random numbers
Therefore, we still want the weights to be very close to zero, but as we have argued above, not identically zero. But it’s not necessarily the case that smaller numbers will work strictly better. For example, a Neural Network layer that has very small weights will during backpropagation compute very small gradients on its data (since this gradient is proportional to the value of the weights).

### Calibrating the variances with 1/sqrt(n)
The distribution of the outputs from a randomly initialized neuron has a variance that grows with the number of inputs. Calibration ensures that all neurons in the network initially have approximately **the same output distribution** and empirically improves the rate of convergence.

### Initializing the biases
It is possible and common to initialize the biases to be zero, since the asymmetry breaking is provided by the small random numbers in the weights. 

### In practice
The current recommendation is to use ReLU units and use the `w = np.random.randn(n) * sqrt(2.0/n)`.

### Batch Normalization
Explicitly forcing the activations throughout a network to take on a unit gaussian distribution at the beginning of the training.

## Regularization
There are several ways of controlling the capacity of Neural Networks to prevent over:

### L2 regularization
The L2 regularization has the intuitive interpretation of heavily penalizing peaky weight vectors and preferring diffuse weight vectors.

### L1 regularization
It has the intriguing property that it leads the weight vectors to become sparse during optimization. In other words, neurons with L1 regularization end up using only a sparse subset of their most important inputs and become nearly invariant to the “noisy” inputs. 

### Max norm constraints
Clamping the weight vector $W$ of every neuron to satisfy $||W||_2 < c$. Typical values of $c$￼are on orders of 3 or 4. One of its appealing properties is that network cannot “explode” even when the learning rates are set too high because the updates are always bounded.

### Dropout
While training, dropout is implemented by only keeping a neuron active with some probability $p$ (a hyperparameter), or setting it to zero otherwise.

![](/images/CS231n-Note-Neural-Networks-Part-2-f4.png)

### Bias regularization
It is not common to regularize the bias parameters because they do not interact with the data through multiplicative interactions, and therefore do not have the interpretation of controlling the influence of a data dimension on the final objective.

