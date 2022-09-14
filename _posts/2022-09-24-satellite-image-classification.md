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
On [Twitter](https://twitter.com/robmarkcole) & [LinkedIn](https://www.linkedin.com/in/robmarkcole/) I regularly post on the topic of deep learning applied to satellite & aerial imagery, and I receive many messages from people who want to get started training models but are unsure where to begin. I maintain a popular repository on Github called the [satellite-image-deep-learning](https://github.com/robmarkcole/satellite-image-deep-learning) which lists many useful references, ranging from very introductory articles to the code for cutting edge techniques published in the academic literature. However this long list of references is not necessarily that approachable to people getting started, so I am going to publish a series of 'Getting started with ..' blog posts addressing the techniques listed in my repository. This first post is on image classification of satellite imagery, which has many practical applications and is ideal for practicing the basics of deep learning. Lets get started!

## What is image classification?
You may already be familiar with image classification from seeing the numerous cats vs dogs image classification tutorials on the internet. Image classification is therefore the task of assigning a label to an image, or even assigning multiple labels to an image[^1]. When applied to satellite imagery, classification has two common uses:

- label the dominant subject of image, e.g. golf course, harbour
- perform binary detection of some subject, e.g. ship present or not, deforested or not

To get more familiar with this task I recommend exploring a couple of benchmark image classification datasets[^2], such as the UC Merced dataset (a sample of which is shown below) or the EuroSAT dataset. Both of these datasets are available in the standard RGB/single label format, but also in more interesting multi-class versions. For these and other datasets see the [Datasets](https://github.com/robmarkcole/satellite-image-deep-learning/blob/master/assets/datasets.md) section on my repository.

![](https://www.researchgate.net/publication/324924412/figure/fig4/AS:644015246544898@1530556608631/Example-images-from-the-UC-Merced-dataset.png "The UC merced dataset")

## Which models are used for classification?
The [Classification](https://github.com/robmarkcole/satellite-image-deep-learning#classification) section in my repository lists many different resources demonstrating the training of classification models on satellite imagery. In fact it is relatively rare to train a model from scratch on your own dataset, and far more common to use a model that has been pre-trained on a benchmark dataset (usually Imagenet) and then fine-tune this model on your own dataset. To learn more about fine-tuning I recommend the [fine-tuning lesson on d2l.ai](https://d2l.ai/chapter_computer-vision/fine-tuning.html). So assuming your are going to fine-tune a model your fist choice is which model to select. 

The internet regularly reports new 'state of the art' models which improve performance on some benchmark dataset or other, and it would be reasonable to assume that you should choose the latest and greatest model. However for an approachable article comparing models I highly recommend reading [The best vision models for fine-tuning](https://www.kaggle.com/code/jhoward/the-best-vision-models-for-fine-tuning/notebook) by Jeremy Howard. In this article Jeremy compares 86 models on two benchmark datasets; the [IIT Pet dataset](https://www.robots.ox.ac.uk/~vgg/data/pets/) and the [Kaggle Planet dataset](https://www.kaggle.com/c/planet-understanding-the-amazon-from-space/data) (a remote sensing dataset). He shows that the modern models (convnext and vit) are indeed the top performers in terms of accuracy. Interestingly the best performers vary between the Pets and Planet datasets, and Jeremy attributes this to the fact that the Planet dataset does not resemble the images in the ImageNet dataset (which most models are pre-trained on), so the models which learn new features the fastest are the best performers on Planet. He also notes that "there's little correlation between model size and performance" on the Planet dataset, and advises selecting smaller models due to this (which will also be faster in use). An additional advantage of choosing a small model is that the pace of experimentation is faster. For me a surprising result on the Planet dataset is that the Resnet 18 model ([published in 2015](https://arxiv.org/abs/1512.03385)) is in the top 10 performers (shown below). As Jeremy says, "Resnet 18 has very low memory use, is fast, and is still quite accurate", and for these reasons I suggest it is a good default model to begin projects with.

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/classification/table.png "The top 10 performers on the Planet dataset")

## Your first end-to-end classification project
Perhaps you already have a use case for classification from your day job, but if not I suggest deciding on a topic that interests you (e.g. deforestation, crop classification) and finding a relevant dataset on Kaggle or in my repository. Begin by following a tutorial on fine-tuning a vision model (e.g. the [fine-tuning lesson on d2l.ai](https://d2l.ai/chapter_computer-vision/fine-tuning.html)) and then adapt it to use your chosen dataset. You will probably encounter some challenges just from switching dataset alone, such as dealing with different formats of data (e.g. png vs geotiff), and different sized images or number of channels. You will probably have to modify the code for loading and preprocessing the dataset, and this is a good opportunity to practice your python skills and get familiar with your deep learning framework (Tensorflow or Pytorch). You can then begin experimenting to see what factors affect model performance you can achieve, and experiment with data augmentation strategies and training parameters to improve model performance. I also recommend reading about under and over-fitting, and perform some experiments to demonstrate these phenomenon so that you will recognise them when they occur. 

Once you have gained confidence training and tuning a model on a published dataset, I recommend next creating your own dataset. An classification dataset can be created by downloading images from Google Earth, using one of the scripts listed on my repository [here](https://github.com/robmarkcole/satellite-image-deep-learning/blob/master/assets/software.md#image-dataset-creation). To prepare the dataset for training it will be necessary to sort your images into folders where the folder name is the label that will be used for that class. Fortunately this can be done using just the file browser on your computer, and no 'annotation' software is required. Aim to have an equal number of images in each folder, so that your dataset is balanced. Even so you will probably discovery that your model performance is not uniform across all classes, and you should use a confusion matrix to identify this imbalance. An example is shown below:

![](https://www.researchgate.net/publication/340154539/figure/fig5/AS:873000131891200@1585150859016/The-confusion-matrix-of-the-identifying-results-based-on-remote-sensing-images.ppm "Confusion matrix showing how model accuracy varies across classes")

Be sure to create training, validation and test datasets, and to report final metrics on the test dataset only. Having completed this process you will have demonstrated an end-to-end project which you could then write a blog post about, or share with colleagues. 


## Footnotes
[^1]: When there are **more** than one label to be associated with an image the task is usually referred to as 'multi-class' or 'multi-label' classification. This more complex task is beyond the scope of this post but I aim to revisit in a later post. If you are keen to explore this topic already checkout the Medium article [Multi-label Land Cover Classification with Deep Learning](https://towardsdatascience.com/multi-label-land-cover-classification-with-deep-learning-d39ce2944a3d)
[^2]: A benchmark dataset is a dataset that is used as a standard by the community to compare the performance of different techniques
