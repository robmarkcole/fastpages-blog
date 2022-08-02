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
I will admit that whenever I hear Transformers, the first image that flashes through my mind is that of the cartoon characters I remember from my childhood in the 1980's. And whilst that was, and continues to be a great TV & film series, the Transformers I wish to talk about are those making waves in the deep learning community. So first things first, what is a Transformer? The Transformer is a neural network architecture first published in a 2017 paper titled [Attention Is All You Need](https://arxiv.org/abs/1706.03762) by researchers at Google. Transformers learn context by tracking relationships in sequential data using a technique called attention. Transformers are replacing CNN's and RNN's in many applications and have come to dominate the field of natural language processing[^1]. Recently I have started seeing remote sensing publications using Transformers, and I became curious about the impact they are having in this community. I Tweeted about this topic and got many interesting responses:

<blockquote class="twitter-tweet tw-align-center"><p lang="en" dir="ltr">What questions do people have about Transformers and their use in remote sensing? This is the topic of my next blog post 🙇‍♂️🚀</p>&mdash; Robin Cole (@robmarkcole) <a href="https://twitter.com/robmarkcole/status/1554348041926311937?ref_src=twsrc%5Etfw">August 2, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

To paraphrase the questions asked:
- What are the advantages of Transformers in classification/segmentation/object detection?
- Do they require more training data than CNN's?
- Are they harder to train than CNN's?
- Are there significant engineering tradeoffs in using Transformers?

## Footnotes
[^1]: https://blogs.nvidia.com/blog/2022/03/25/what-is-a-transformer-model/