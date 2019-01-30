---
layout: post
title: Domain adaptation for semantic segmentation
---


## Motivation

Given an annotated semantic segmentation dataset, the task is to use these annotations to supervise the semantic segmentation of another dataset. 

There are two apporaches to domain adaptation for semantic segmentation in general. One is to transfer the source dataset to target dataset in image level or feature level. Another approach uses self-training, which first assign proxy labels for the target dataset and then correct the labels with the annotations on source dataset.


## Apporach 1: Self training approaches

#### 1. Adaptive Semantic Segmentation with a Strategic Curriculum of Proxy Labels

1.1 Adaptive Segmentation Architecture

First, the authors use an encoder to learn information from both labeled and unlabeled data. From there they use two branches of decoders to generate predictions of sementic segmentation. They take an agreement map based on the output of the two decoders. If the labels of a pixel from the two segmentations agree with each other, they consider this as an easy pixel. Otherwise, it is a hard pixel. 

To avoid two decoders learning very similar projections, a penalty using cosine similarity between filters in two decoders is added to objective function.

2. Strategic Curriculum

2.1 Weight Loss

Problem of self-training: biased towards majority class
Solution: use a loss weighting vector lambda to assign heavier weights to minority classes. Median inverse frequency is typically used but this paper doubles weights for some classes.

2.2 Target Easy Mining

Mask out gradient from hard pixels.

2.3 Source Hard Mining

Randomly masking gradients of easy pixels from the source domain.

3. Experiment details

* Encoder: ResNet-18
* Feature map at bottleneck: dilated by factor of 4
* Decoder: Pyramid Pooling Modules (PPM)



#### 2. Domain Adaptation for Semantic Segmentation via Class-Balanced Self-Training

#### 1. Self-training (ST) with Self-Paced Learning

The objective is to train a segmentation network with weights w such that segmented source images agree with their ground truth labels, and that segmentated target images agree with their pseudo labels.

Two iterative steps:

a) Update w based on the objective mentioned above.
b) Assign pseudo labels to target images. The assignedment is based on the output of w from step a) with the highest probability.

Note that to enforce the pseudo labels not to be sparse with negative L1 regularization to prevent the trivial solution of ignoring all pseudo-labels. This regularization term has a coefficient so that they can have control over the amount of ignored pseudo labels (larger multiplier means use more pseudo labels for training).

#### 2. Class-balanced self-training (CBST)

To balance the bias towards majority classes, CBST modifies the above iterative steps with a multiplier for each class. A class with a larger coefficient will have more images used for training.

#### 3. Spatial priors (CBST-SP)

This paper use normalized frequency of each class as spatial priors and multiplies the priors to the output of segmentation network.








## Apporach 2: Domain transfer in image/feature level

#### 1. Domain Stylization: A Strong, Simple Baseline for Synthetic to Real Image Domain Adaptation

This paper presents an iterative algorithm. Iterative between training two networks:

a. Domain Stylization (DS):

Generate an image that has the semantic information from a source image and in the style of a target image.

b. Semantic Segmentation Learning (SSL):

Predict semantic segmentation from the image generated in DS step. Since we have ground truth segmentation for source dataset, if the DS step is successful, then the SSL learned on the stylized source image should have the capability to correctly segment images in the target domain.

##### Experiment details

* DS step uses FastPhotoStyle.
* They use N=10 randomly selected target images to provide style information in DS step.
* Empirically two iterations are enough.




