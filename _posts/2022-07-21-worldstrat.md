---
title: "The WorldStrat Dataset"
description: "Quick tour of the WorldStrat dataset"
layout: post
categories: [markdown]
toc: true
image: images/worldstrat/main.jpg
show_image: true
hide: false
---
# The WorldStrat Dataset

A new dataset called the WorldStrat dataset was this week announced on Twitter by Julien Cornebise and colleagues. The release includes a paper on arXiv[^1], code on Github[^2]:, and the dataset itself on both Zenodo[^3] and Kaggle[^4]. 

<blockquote class="twitter-tweet tw-align-center"><p lang="en" dir="ltr">Proud to release the WorldStrat dataset with <a href="https://twitter.com/ivanorsolic?ref_src=twsrc%5Etfw">@ivanorsolic</a> <a href="https://twitter.com/alkalait?ref_src=twsrc%5Etfw">@alkalait</a> and <a href="https://twitter.com/esa?ref_src=twsrc%5Etfw">@esa</a> Φ-lab:<br>- ~10,000 km² of high-res SPOT satellite imagery<br>- Multi-temporal matched low-res Sentinel2 images<br>- Stratified wrt global land-uses<br>- Enriched with sites under-represented in ML<br>🧵1/9 <a href="https://t.co/kR0AnzIlkg">pic.twitter.com/kR0AnzIlkg</a></p>&mdash; Julien Cornebise (@JCornebise) <a href="https://twitter.com/JCornebise/status/1549356696664956928?ref_src=twsrc%5Etfw">July 19, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This dataset is significant for a number of reasons:

- Greater than 100 GB of imagery with global coverage
- Covers locations typically under-represented in ML datasets
- Colocated low and high resolution imagery
- Code provided to extend the dataset
- Models & tutorials provided

The dataset comprises Sentinel 2 timeseries & colocated high resoluton Airbus SPOT imagery providing 10 & 1.5 m/pixel respectively. An example is shown below:

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/worldstrat/fields.jpg "Fields" )

# Super resolution
The colocated low and high resolution imagery enables the training of super resolution models

# Footnotes
[^1]: Paper on [arXiv](https://arxiv.org/abs/2207.06418)
[^2]: Code [on Github](https://github.com/worldstrat/worldstrat)
[^3]: The full 107 GB dataset is [hosted on Zenodo](https://zenodo.org/record/6810792#.YtjNb-zMK3I)
[^4]: A 53 GB version of the dataset [is on Kaggle](https://www.kaggle.com/datasets/jucor1/worldstrat). 

