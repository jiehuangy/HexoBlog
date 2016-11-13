---
title: '[CS231n Note] Linear classification: SVM, Softmax'
date: 2016-11-10 00:58:04
tags:
categories: Neural Networks
---
![Example of the difference between the SVM and Softmax classifiers for one datapoint](/images/Note-CS231n-Linear-classification-SVM-Softmax-f1.png)
<!-- more -->

Last section descibes the problem of Image Classification and solve the problem with KNN. In this section, we describes linear approach for Image Classification. The approach contains two components: **score function** and **loss function**

- Linear Score Function: map the pixel values of an image to scores for each class. $f(x_i,W,b) = Wx_i+b$



- Loss Function: measure our unhappiness with outcomes with a loss function (or the cost function or the objective).


## Multiclass Support Vector Machine

### Score function
The score is interpreted as confidence score. The class with highest value is the predicted result.

### Loss function
The SVM loss is set up so that the SVM “wants” the correct class for each image to a have a score higher than the incorrect classes by some $\Delta$. The Multiclass SVM loss for the i-th example is then formalized as follows:


{% math %} 
\begin{aligned}
L_i  & =  \sum_{j\neq y_i}max(0,s_i - s_{y_i} +\Delta) \\
& =  \sum_{j\neq y_i}max(0,w_j^Tx_i - w_{y_i}^Tx_i +\Delta)
\end{aligned}
{% endmath %}

the threshold at zero function is often called the **hinge loss**.

### Regularization
 If some parameters $W$ correctly classify all examples (so loss is zero for each example), then any multiple of these parameters $\lambda W$ where $\lambda$ will also give zero loss. We wish to encode some preference for a certain set of weights W over others to remove this ambiguity. The full loss becomes:

 {% math %}
L=\underbrace{\dfrac{1}{N}\sum_{i}L_i}_{data loss} + \underbrace{\lambda R(W)}_{regularization loss}
 {% endmath %}

 Advantages of regularization:
 - remove the ambiguity of $W$.
 - improve generalization, because it means that no input dimension can have a very large influence on score.
 - L2 penalty leads to the appealing max margin property.

## Softmax classifier

### Score function
Interpret the scores function $f(x_i;W)=Wx_i$ as the unnormalized log probabilities for each class.

### Loss function
Replace the **hinge loss** with a **cross-entropy loss**.


 {% math %}
L_i=-log(\dfrac{e^{f_{y_i}}}{\sum_{j}e^{f_j}})
 {% endmath %}

#### Information theory interpratation
The cross-entropy between a “true” distribution ￼ and an estimated distribution.
 {% math %}
H(p,q) = -\sum_{x}p(x)logq(x)
 {% endmath %}
Moreover, since the cross-entropy can be written in terms of entropy and the Kullback-Leibler divergence as {% math %} H(p,q) = H(p)+D_{KL}(p||q){% endmath %}, and the entropy of the $H(p)$ is zero, this is also equivalent to minimizing the KL divergence between the two distributions.

### Probability interpretation
The (normalized) probability assigned to the correct label $y_i$ given the image $x_i$ and parameterized by $W$.
 {% math %}
p(y_i|x_i;W)=\dfrac{e^{f_{y_i}}}{\sum_{j}e^{f_j}}
 {% endmath %}
In the probabilistic interpretation, we are therefore minimizing the negative log likelihood of the correct class, which can be interpreted as performing Maximum Likelihood Estimation (MLE).

Besides, we can now also interpret the regularization term $R(W)$ in the full loss function as coming from a Gaussian prior over the weight matrix $W$, where instead of MLE we are performing the Maximum a posteriori (MAP) estimation.

## SVM vs. Softmax
The Softmax classifier is never fully happy with the scores it produces: the correct class could always have a higher probability and the incorrect classes always a lower probability and the loss would always get better. However, the SVM is happy once the margins are satisfied and it does not micromanage the exact scores beyond this constraint.






