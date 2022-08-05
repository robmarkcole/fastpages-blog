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
I will admit that whenever I hear Transformers, the first image that flashes through my mind is that of the cartoon characters I remember from my childhood in the 1980's. And whilst that was, and continues to be a great TV & film series, the Transformers I wish to talk about are those making waves in the deep learning community. So first things first, what is a Transformer? The Transformer is a neural network architecture first published in a 2017 paper titled [Attention Is All You Need](https://arxiv.org/abs/1706.03762) by researchers at Google. Transformers learn context by tracking relationships in sequential data using a technique called *attention*. Transformers are replacing CNN’s and RNN’s in many applications and have come to dominate the field of natural language processing[^1] in only a few years.

Transformers were successfully applied to imagery in the 2020 paper [An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale](https://arxiv.org/abs/2010.11929), again by researchers at Google. Transformers applied to vision are commonly referred to as Vision Transformers, or ViT. I will not go deep into deep technical details here since those are covered in the paper and elsewhere, but the first figure from the paper is worth reproducing here along with a basic explanation of the core features of ViT's:

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/transformers/paper_fig1.jpg "Figure 1 from An Image is Worth 16x16 Words")

The caption from the figure above explains: *We split an image into fixed-size patches, linearly embed each of them, add position embeddings, and feed the resulting sequence of vectors to a standard Transformer encoder. In order to perform classification, we use the standard approach of adding an extra learnable “classification token” to the sequence.* We can see that there are absolutely **no convolutional layers**, and the authors note that the ViT *has much less image-specific inductive bias than CNNs. In CNNs, locality, two-dimensional neighborhood structure, and translation equivariance are baked into each layer throughout the whole model. In ViT, only MLP layers are local and translationally equivariant, while the self-attention layers are global.* This results in ViT's requiring larger data volumes to achieve comparable levels of performance to CNN's. Indeed a ViT trained on ImageNet (1M images), under-performs a CNN. However with significantly larger data volumes (300M images), the ViT outperforms the CNN. Also a ViT is able to capture more global relationships in an image, which hints at their potential benefits when applied to remote sensing imagery. Note that in practice it is typical to fine tune a ViT that has been pre-trained, just as we usually do with a CNN.

## Transformers in remote sensing
Relatively recently I have started noticing greater numbers of remote sensing publications using Transformers. I became curious about the level of interest and understanding of Transformers in the remote sensing community, and a Tweet about this got many responses:

<blockquote class="twitter-tweet tw-align-center"><p lang="en" dir="ltr">What questions do people have about Transformers and their use in remote sensing? This is the topic of my next blog post 🙇‍♂️🚀</p>&mdash; Robin Cole (@robmarkcole) <a href="https://twitter.com/robmarkcole/status/1554348041926311937?ref_src=twsrc%5Etfw">August 2, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

To paraphrase the questions asked:
- Do Transformers have the best performance on common remote sensing tasks?
- Do they require more training data?
- Is there a minimum data volume requirement?
- Are they harder to train?
- Are there significant engineering tradeoffs in using Transformers?
- Are transformers of any use for tabular remote sensing data?

### Performance
To begin addressing these questions I will first reference the 2022 paper [Current Trends in Deep Learning for Earth Observation: An Open-source Benchmark Arena for Image Classification](add url). This paper compares compares the performance of vision transformers (ViT's) with eight other neural network architectures on the task of classification. Figure 1 from that paper is shown below:

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/transformers/classification.jpg "Figure 1 from Current Trends in Deep Learning for Earth Observation")

This paper provides a useful overview of multiple classification datasets, shown in (a) above. The datasets range considerably in number of images and classes. Model performance is compared on (b) multi-label and (c) multi-class classification tasks. The darker shaded bars are performance when a model is trained from scratch, and the lighter shading bars are performance when the model is pre-trained on the ImageNet-1K dataset. We immediately observe that pre-training always improves model performance, which is a very useful takeaway. Amongst the models, ViT and DenseNet are the best performers, although ViT actually performs *worst* on the largest dataset, BigEarthNet. It is also interesting that for many of the datasets, the commonly used ResNet achieves comparable performance.

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