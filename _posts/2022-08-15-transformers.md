---
title: "Transformers in remote sensing"
description: "Introduction to Transformers and their use in remote sensing"
layout: post
categories: [markdown]
toc: true
image: images/transformers/transformer.jpg
show_image: true
hide: false
comments: true
---

## Introduction
paper on arXiv[^1]

# Deep dive: UNetFormer
- Title: A UNet-like transformer for efficient semantic segmentation of remote sensing urban scene imagery
- Paper: https://arxiv.org/abs/2109.08937
- Code: https://github.com/WangLibo1995/GeoSeg
- Datasets: ISPRS Vaihingen and Potsdam & LoveDA used

**What’s a Transformer Model?:** a neural network architecture published in a 2017 paper titled [Attention Is All You Need](https://arxiv.org/abs/1706.03762). Transformers learn context by tracking relationships in sequential data using a technique called attention. Transformers are replacing CNNs and RNNs in many applications and have come to dominate the field of natural language processing (NLP). [Ref and further reading](https://blogs.nvidia.com/blog/2022/03/25/what-is-a-transformer-model/)

**What’s new here?:** semantic segmentation has typically been tackled using a Fully Convolutional Network (FCN) with an
encoder-decoder architecture (i.e. U-net) employing a ResNet (or similar) backbone. The encoder generates multi-level feature maps which are incorporated into the final prediction by a decoder.
**What are the results?:** 

**My thoughts:** given the significant impact of Transformers on NLP, their use in vision could lead to new breakthroughs in semantic segmentation accuracy. One issue I have experienced with transformers is that they can use a lot of RAM, so in practice improved accuracy may come at the expense of performance and cost. I suspect that U-net will remain 'good enough' for a while longer

**Further reading:**
- [BIT_CD](https://github.com/justchenhao/BIT_CD) is a change detection model using transformers

## Footnotes
[^1]: https://arxiv.org/abs/2207.06418
