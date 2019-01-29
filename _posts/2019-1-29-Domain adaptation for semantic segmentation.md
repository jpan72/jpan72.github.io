---
layout: post
title: Domain adaptation for semantic segmentation
---


## Motivation

Given an annotated semantic segmentation dataset, the task is to use these annotations to supervise the semantic segmentation of another dataset. 

There are two apporaches to domain adaptation for semantic segmentation in general. One is to transfer the source dataset to target dataset in image level or feature level. Another approach uses self-training, which first assign proxy labels for the target dataset and then correct the labels with the annotations on source dataset.


