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

Checkout available [optimizers](https://github.com/fchollet/keras/blob/master/keras/optimizers.py) in Keras.
