---
layout: post
title: Domain adaptation for semantic segmentation
---


## Motivation

Given an annotated semantic segmentation dataset, the task is to use these annotations to supervise the semantic segmentation of another dataset. 

There are two apporaches to domain adaptation for semantic segmentation in general. One is to transfer the source dataset to target dataset in image level or feature level. Another approach uses self-training, which first assign proxy labels for the target dataset and then correct the labels with the annotations on source dataset.


### Apporach 1: Self training approaches

#### 1. Adaptive Semantic Segmentation with a Strategic Curriculum of Proxy Labels

##### a) Adaptive Segmentation Architecture

First, the authors use an encoder to learn information from both labeled and unlabeled data. From there they use two branches of decoders to generate predictions of sementic segmentation. They take an agreement map based on the output of the two decoders. If the labels of a pixel from the two segmentations agree with each other, they consider this as an easy pixel. Otherwise, it is a hard pixel. 
