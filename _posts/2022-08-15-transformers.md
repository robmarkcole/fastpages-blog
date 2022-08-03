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
I will admit that whenever I hear Transformers, the first image that flashes through my mind is that of the cartoon characters I remember from my childhood in the 1980's. And whilst that was, and continues to be a great TV & film series, the Transformers I wish to talk about are those making waves in the deep learning community. So first things first, what is a Transformer? The Transformer is a neural network architecture first published in a 2017 paper titled [Attention Is All You Need](https://arxiv.org/abs/1706.03762) by researchers at Google. Transformers learn context by tracking relationships in sequential data using a technique called attention. Transformers are replacing CNN's and RNN's in many applications and have come to dominate the field of natural language processing[^1]. Transformers were then applied to imagery in the paper [An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale](https://arxiv.org/abs/2010.11929). Transformers applied to vision are referred to as Vision Transformers, or ViT. I will not go deep into deep technical details here since those are covered in detail in the paper and elsewhere, but the first figure from the paper is worth reproducing here.

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/transformers/paper_fig1.jpg "Figure 1 from An Image is Worth 16x16 Words" )


## Transformers in remote sensing
Relatively recently I have started seeing greater numbers of remote sensing publications using Transformers. I became curious about the level of interest and understanding of in the remote sensing community, and a Tweet about this got many interesting responses indicating a high level of interest:

<blockquote class="twitter-tweet tw-align-center"><p lang="en" dir="ltr">What questions do people have about Transformers and their use in remote sensing? This is the topic of my next blog post 🙇‍♂️🚀</p>&mdash; Robin Cole (@robmarkcole) <a href="https://twitter.com/robmarkcole/status/1554348041926311937?ref_src=twsrc%5Etfw">August 2, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

To paraphrase the questions asked:
- What are the advantages of Transformers in classification/segmentation/object detection?
- Do they require more training data than CNN's?
- Are they harder to train than CNN's?
- Are there significant engineering tradeoffs in using Transformers?
- Are transformers of any use for tabular remote sensing data?

## Footnotes
[^1]: https://blogs.nvidia.com/blog/2022/03/25/what-is-a-transformer-model/