---
title: "Notice on optimizers"
categories:
  - deep-learning
tags:
  - deep-learning
  - optimizers
  - keras
---

Short recall on SGD, Adam, AdaDelta, RMSProp.

Notations :

* G - gradient
* lr - learning rate
* theta - parameter to update

## SGD

```
lr <- lr * 1.0/(1.0 + decay * n_iterations)
M <- mu * M - lr * G
```

a) ordinary

```
theta <- theta - lr * G + mu * M
```

b) with nesterov moment
```
theta <- theta - lr * G + (mu * M - lr * G) * mu
```

## RMSProp = gradient over RMS

```
lr <- lr * 1.0/(1.0 + decay * n_iterations)
```

RMS (^2) = Mean square gradient
```
A <- rho * A + (1 - rho) * G^2
theta <- theta - lr * G / (sqrt(A) + eps)
```
- Reference: T. Tieleman and G. Hinton.   Divide the gradient by a running average of its recent magnitude.  COURSERA: Neural Networks for Machine Learning, 4, 2012.

In lot of papers (e.g. [[1]](https://arxiv.org/pdf/1512.00567v3.pdf) or [[2]](https://arxiv.org/pdf/1707.07012.pdf)) authors use this optimizer with parameters: 
```
rho = 0.9
eps = 1.0
```

## AdaDelta = gradient proportional previous update over RMS

```
lr <- lr * 1.0/(1.0 + decay * n_iterations)
```

RMS (^2) = Mean square gradient
```
A <- rho * A + (1 - rho) * G^2
U <- G * sqrt(dA + eps)/ (sqrt(A + eps))
theta <- theta - lr * U
dA <- rho * dA + (1 - rho) * U
```

## Adam = cumulative gradient over RMS
```
lr <- lr * 1.0/(1.0 + decay * n_iterations)
t <- n_iterations + 1
lr <- lr * sqrt(1 - beta_2 ^ t)/sqrt(1 - beta_1 ^ t)
```

RMS (^2) = Mean square gradient
```
A <- beta_2 * A + (1 - beta_2) * G^2
M <- beta_1 * M + (1 - beta_1) * G
theta <- theta - lr * M / (sqrt(A) + eps)
```

Default parameters : 
```
beta_1 = 0.9 
beta_2 = 0.999
eps = 1e-8
```
and choosing `beta_1 = 0.0` we obtain RMSProp optimization.

## Links:
- Checkout available [optimizers](https://github.com/fchollet/keras/blob/master/keras/optimizers.py) in Keras.
- Checkout [optimizers](http://pytorch.org/docs/master/optim.html#algorithms) in PyTorch.

