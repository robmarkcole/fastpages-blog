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

## Which models are used for classification?
The [Classification](https://github.com/robmarkcole/satellite-image-deep-learning#classification) section in my repository lists many different models for classification of satellite imagery, but the typically approach is to select a model that has been pre-trained on a benchmark dataset (usually Imagenet) and then fine tune this model on your own dataset. The academic literature regularly reports new 'state of the art' models which improve performance on some benchmark dataset or other. For an up to date and approachable resource comparing models I highly recommend reading the article [The best vision models for fine-tuning](https://www.kaggle.com/code/jhoward/the-best-vision-models-for-fine-tuning/notebook) by Jeremy Howard. In this article Jeremy compares 86 models on two benchmark datasets; the [IIT Pet dataset](https://www.robots.ox.ac.uk/~vgg/data/pets/) and the [Kaggle Planet dataset](https://www.kaggle.com/c/planet-understanding-the-amazon-from-space/data) (a remote sensing dataset). He shows that the modern models (convnext and vit) are the top performers, and demonstrates the tradeoff between speed and accuracy which should factor into your decision making when selecting a model. Interestingly the best performers vary between the Pets and Planet datasets, and Jeremy attributes this to the fact that the Planet dataset does not resemble the images in the ImageNet dataset (which the models are pre-trained on), so the models which learn new features the fastest are the best performers on Planet. He also notes that "there's little correlation between model size and performance" on the Planet dataset, and advises selecting smaller models due to this (which will be faster in use). An additional advantage of choosing a small model is that the pace of iteration is faster, enabling more experimentation in a given time-frame. A striking result on the Planet dataset is that the 'classic' Resnet 18 model is in the top 10 performers (shown below). As Jeremy says, "Resnet 18 has very low memory use, is fast, and is still quite accurate", and for these reasons I suggest it is a good default model to begin experimentation with.

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/classification/table.png "The top 10 performers on the Planet dataset")

## Inspiration for your first classification project
Perhaps you already have a use case for classification in your day job, but if not I suggest selecting a problem that interests you (e.g. deforestation, crop classification) and first finding a related dataset on Kaggle and begin working through some of the notebooks using that dataset. You will probably quickly settle on your preferred deep learning framework (tensorflow, pytorch etc) and can then begin experimenting to see if you can improve on the published results. As shown in the above section, simply selecting a different model can result in improved performance. You can also experiment with data augmentation and hyperparameter tuning of the models. Once you have gained confidence training and tuning a model on this dataset, I recommend creating your own dataset. 

## Footnotes
[^1]: When there are **more** than one label to be associated with an image the task is usually referred to as 'multi-class' or 'multi-label' classification. This more complex task is beyond the scope of this post but I aim to revisit in a later post. If you are keen to explore this topic already checkout the Medium article [Multi-label Land Cover Classification with Deep Learning](https://towardsdatascience.com/multi-label-land-cover-classification-with-deep-learning-d39ce2944a3d)
[^2]: A benchmark dataset is a dataset that is used as a standard by the community to compare the performance of different techniques
