---
title: "Transformers in remote sensing"
description: "Introduction to Transformers and why you should care"
layout: post
categories: [markdown]
toc: true
image: images/transformers/transformer.jpg
show_image: true
hide: true
comments: true
---

## Introduction
Whenever I hear Transformers the first image that flashes through my mind is that of the cartoon characters I remember from my childhood in the 1980's. And whilst that was a great TV series, the Transformers I wish to talk about are those making waves in the deep learning community. So first things first, what is a Transformer? The Transformer is a neural network architecture first published in a 2017 paper titled [Attention Is All You Need](https://arxiv.org/abs/1706.03762) by researchers at Google. Transformers learn context by tracking relationships in sequential data using a technique called *attention*. Transformers are replacing CNN’s and RNN’s in many applications and have come to dominate the field of natural language processing[^1] in only a few years. 

Transformers were successfully applied to imagery in the 2020 paper [An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale](https://arxiv.org/abs/2010.11929), again by researchers at Google. Transformers applied to vision are commonly referred to as Vision Transformers, or ViT. I will not go into deep technical details here since those are covered in the paper and elsewhere, but the first figure from the paper is worth reproducing:

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/transformers/paper_fig1.jpg "Figure 1 from An Image is Worth 16x16 Words. The caption from the figure explains: We split an image into fixed-size patches, linearly embed each of them, add position embeddings, and feed the resulting sequence of vectors to a standard Transformer encoder. In order to perform classification, we use the standard approach of adding an extra learnable 'classification token' to the sequence.")

We can see that there are absolutely **no convolutional layers**, and the authors note that the ViT *has much less image-specific inductive bias[^2] than CNNs.* The authors suggest this is why ViT require larger data volumes to achieve comparable levels of performance to CNN's. They find that a ViT trained from scratch on ImageNet (1M images) under-performs a CNN. However on training with a significantly larger data volume (300M images), the ViT outperforms the CNN owing to its ability to capture greater context. Note that in practice it is typical to fine tune a ViT that has been pre-trained, just as we usually do with a CNN.

## Transformers in remote sensing
Recently I have noticed greater numbers of remote sensing publications using Transformers/ViT. I became curious about the level of interest in Transformers in the remote sensing community and a Tweet about this got some interesting responses:

<blockquote class="twitter-tweet tw-align-center"><p lang="en" dir="ltr">What questions do people have about Transformers and their use in remote sensing? This is the topic of my next blog post 🙇‍♂️🚀</p>&mdash; Robin Cole (@robmarkcole) <a href="https://twitter.com/robmarkcole/status/1554348041926311937?ref_src=twsrc%5Etfw">August 2, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

To paraphrase the main questions asked:
- Do Transformers have the best performance?
- Do they require more training data?
- Are they harder to train?

I have subsequently come to appreciate there are not definitive answers to these questions, and issues such as performance/dataset size/training complexity are all coupled. Nevetheless I attempt to answer each of these in turn below.

## Performance
To begin addressing these questions I will first reference the 2022 paper [Current Trends in Deep Learning for Earth Observation: An Open-source Benchmark Arena for Image Classification](https://arxiv.org/abs/2207.07189). This paper compares the performance of vision Transformers (ViT) with eight other neural network architectures on the task of classification. Figure 1 from that paper is shown below:

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/transformers/classification.jpg "Figure 1 from Current Trends in Deep Learning for Earth Observation")

This paper provides a useful overview of multiple classification datasets, shown in (a) above. The datasets range considerably in number of images and classes. Model performance is compared on (b) multi-label and (c) multi-class classification tasks. The darker shaded bars are performance when a model is trained from scratch, and the lighter shading bars are performance when the model is pre-trained on the ImageNet-1K dataset. We immediately observe that **pre-training almost always improves model performance**, which is a very useful takeaway. Amongst the models, **ViT and DenseNet are the best performers**, although ViT actually performs *worst* on the largest dataset, BigEarthNet. It is also interesting that for many of the datasets, a ResNet achieves comparable performance.

## Training data requirements
I think it is a fair assumption that the vast majority of remote sensing users will be using pre-trained models[^3], so I will not discuss any further the requirements for training a ViT from scratch. Referring back to Figure 1, it is clear there is **not** a simple rule of thumb that large data volumes will guarantee better performance with a ViT. A much more likely scenario in practice is that a user has a relatively limited training dataset, and has already trained a CNN and wants to know if it is worth training a ViT. I have actually been unable to find a definitive paper focussing on this scenario, so if you find one please mention in the comments section. There are papers that propose innovations to reduce the training dataset size requirements, for example [using self-supervision](https://arxiv.org/abs/2106.03746). 

## Training difficulty
If we again consider only fine tuning, is training a ViT more difficult than a CNN? To gain first hand experience I worked through [Fine-Tune ViT for Image Classification with Huggingface Transformers](https://huggingface.co/blog/fine-tune-vit)

## Summary
The use of vision Transformers is an area of active research and providing a summary on the overall state of research would be a research paper in itself, and beyond the scope of this blog post. However I hope this post has provided a useful introduction to the novel features of Transformers, and some insight into the practicality of using them. So should you consider using Transformers in your work any time soon? My own assessment is that people should continue to use CNN's and only really consider using a Transformer if they require the highest accuracy (for example if entering a competition), have medium to large datasets available, and a prepared for significant time performing experiments. 

## Further reading
- Original Google [blog post on transformers](https://ai.googleblog.com/2020/12/transformers-for-image-recognition-at.html)
- Pytorch implementation of a ViT: [vit-pytorch](https://github.com/lucidrains/vit-pytorch)
- ArXiv paper: [Formal Algorithms for Transformers](https://arxiv.org/abs/2207.09238)

## Terminology
- CNN: convolutional neural network
- RNN: recurrent neural network
- ViT: vision transformer

## Footnotes
[^1]: https://blogs.nvidia.com/blog/2022/03/25/what-is-a-transformer-model/
[^2]: image-specific inductive bias: in CNN's the use of kernels bakes in the notion that image pixels are locally correlated and their correlation maps are translation-invariant, whilst a ViT must learn this, [ref](https://keras.io/examples/vision/vit_small_ds/)
[^3]: For further reading on pre-training see [An Empirical Study of Remote Sensing Pretraining](https://arxiv.org/abs/2204.02825)