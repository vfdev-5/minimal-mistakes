---
title: "Architecture of some popular Convolutional Neural Network"
categories:
  - deep-learning
tags:
  - cnn
  - VGG16
  - ResNet50
  - DenseNet
  - SqueezeNet
---

In this post I would like to review of some popular convolutional neural network architectures: VGG16, ResNet50, DenseNet, SqueezeNet.
Idea is to provide a simple visual representation and develop an intuition of each architecture. 

### Notations :

- A block of basic operations: convolution, batch normalization, activation etc,
```
--[block]-- 
```
If block reduces input feature maps size, an arrow is drawn:
```
--[block]-->
```

A block of convolution, followed by batch normalization, relu and pooling can be also represented as 
```
--[C|BN|R|P]-->
```

**We do not detail the number of feature maps used at each layer**


## [VGG16](https://github.com/fchollet/keras/blob/master/keras/applications/vgg16.py)

A network with 5 convolutional blocks and 3 fully-connected blocks:
```
input ---[block 1]-->[block 2]--->[block 3]--->[block 4]--->[block 5]-->[flatten]--[FC]--[FC]--[FC]--- output          
          64,64       128,128     256,256,256  512,512,512   512,512,512           4096  4096   X
           
block 1, 2       = -[C|R|C|R|P]-
block 3, 4, 5    = -[C|R|C|R|C|R|P]-
```

## [ResNet50](https://github.com/fchollet/keras/blob/master/keras/applications/resnet50.py)

A network composed roughly of 5 stages. Each stage contains one *convolutional block* and several *identity blocks*:

```
input ---[C|BN|R|P]-->[Stage 2]--->[Stage 3]--->[Stage 4]--->[Stage 5]--->[P]--->[flatten]--->[FC]--- output
          64    
   kernel=7x7   3x3
  stride=(2,2) (2,2) 
  
[Stage 2] = --[CB|a]-->[IdB|b]-->[IdB|c]-->
             
[Stage 3] = --[CB|a]-->[IdB|b]-->[IdB|c]-->[IdB|d]-->

[Stage 4] = --[CB|a]-->[IdB|b]-->[IdB|c]-->[IdB|d]-->[IdB|e]-->[IdB|f]-->

[Stage 5] = --[CB|a]-->[IdB|b]-->[IdB|c]-->


         /--[C|BN]------------------------\
         |  1x1                           |
         |  (2,2)                         |
[CB] = --*--[C|BN|R]-->[C|BN|R]--[C|BN]--(+)--[R]---
            1x1         3x3      1x1 
            (2,2)
            
          /-------------------------------\
          |                               |
[IdB] = --*--[C|BN|R]--[C|BN|R]--[C|BN]--(+)--[R]---
             1x1       3x3       1x1 

```

## [SqueezeNet](https://github.com/rcmalli/keras-squeezenet/blob/master/keras_squeezenet/squeezenet.py)

A small network with AlexNet accuracy. Network is composed of blocks of so-called *fire modules*:

```
input ---[C|R|P]-->[F2]--[F3]--[P]-->[F4]--[F5]--[P]--->[F6]--[F7]--[F8]--[F9]--[Dropout]--[C|R]---[GlobalP]-->[Activation]--- output
  kernel=3x3 3x3               3x3               3x3                                       1x1
 stride=(2,2)(2,2)            (2,2)             (2,2)

                /--[C|R]-----\
                |            |
[F] = ---[C|R]--*--[C|R]--[concat]---
    
```


## [DenseNet](https://github.com/liuzhuang13/DenseNet)

A network that connects feature maps of different levels. Network composed of *dense* and *transition* blocks. 
Here is a variant DenseNet121-BC (Bottleneck-Compressed):

```
input --[C|BN|R|P]-->[DB1(6)]--[TR1]--->[DB2(12)]--[TR2]--->[DB3(24)]--[TR3]--->[DB4(16)]--[GlobalP]--->[FC]-- output
        7x7    3x3
       (2,2)  (2,2)

              /---------------------------\
              |                           |
[DBX(N)] = ---*---[BN|R|C]--[BN|R|C]---[concat]---- x N
                       1x1       3x3


[TR] = --[BN|R|C]---[P]-->
              1x1   2x2
                   (2,2)
```




