---
title: "Getting started with satellite image classification"
description: "A brief introduction to performing classification on satellite & aerial imagery"
layout: post
categories: [markdown]
toc: true
image: images/classification/classification-main.png
show_image: true
hide: true
comments: true
---
## Introduction
On Twitter & LinkedIn I regularly post on the topic of deep learning applied to satellite & aerial imagery, and I receive many messages from people who want to get hands on with this topic but are unsure of how to get started. I maintain a popular repository on Github called the [satellite-image-deep-learning](https://github.com/robmarkcole/satellite-image-deep-learning) which lists many useful references, ranging from very introductory articles on Medium to code for cutting edge techniques published in the academic literature. This has become a very long list of references which is not necessarily approachable to people getting started in this area. Therefore in order to assist these people I am going to publish a series of 'Getting started with ..' blog posts, addressing the techniques listed in my repository. This first post is image classification of satellite imagery, which whilst a conceptually simple technique, actually has many practical applications and is definitely worth mastering before moving onto more exotic tasks such as object detection and semantic segmentation. Lets get started!

## What is image classification?
You will probably already be familiar with image classification from the numerous cats vs dogs image classification tutorials on the internet. Image classification is the task of assigning a label to an image, or even assigning multiple labels to an image[^1]. When applied to satellite imagery, classification may be used to:

- label the dominant subject of image, e.g. golf course, harbour
- perform binary detection of some subject, e.g. ship present or not, deforested or not

If you want to get started training models on a benchmark dataset[^2] I recommend beginning with either the UC merced dataset (a sample of which is shown below) or the EuroSAT dataset. Both of these datasets are available in the standard RGB/single label format, but also in more interesting multi-class versions. For these and other datasets see the [Datasets](https://github.com/robmarkcole/satellite-image-deep-learning/blob/master/assets/datasets.md) section on my repository.

![](https://www.researchgate.net/publication/324924412/figure/fig4/AS:644015246544898@1530556608631/Example-images-from-the-UC-Merced-dataset.png "The UC merced dataset")



## Footnotes
[^1]: When there are **more** than one label to be associated with an image the task is usually referred to as 'multi-class' or 'multi-label' classification. This more complex task is beyond the scope of this post but I aim to revisit in a later post. If you are keen to explore this topic already checkout the Medium article [Multi-label Land Cover Classification with Deep Learning](https://towardsdatascience.com/multi-label-land-cover-classification-with-deep-learning-d39ce2944a3d)
[^2]: A benchmark dataset is a dataset that is used as a standard by the community to compare the performance of different techniques
