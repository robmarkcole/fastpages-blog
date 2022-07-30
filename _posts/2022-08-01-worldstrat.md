---
title: "The WorldStrat Dataset"
description: "Quick tour of the WorldStrat dataset"
layout: post
categories: [markdown]
toc: true
image: images/worldstrat/main.jpg
show_image: true
hide: false
comments: true
---
## Introduction

A new dataset called the WorldStrat dataset was this week announced on Twitter by Julien Cornebise and colleagues. The release includes a paper on arXiv[^1], code on Github[^2], and the dataset itself on both Zenodo[^3] and Kaggle[^4]. 

<blockquote class="twitter-tweet tw-align-center"><p lang="en" dir="ltr">Proud to release the WorldStrat dataset with <a href="https://twitter.com/ivanorsolic?ref_src=twsrc%5Etfw">@ivanorsolic</a> <a href="https://twitter.com/alkalait?ref_src=twsrc%5Etfw">@alkalait</a> and <a href="https://twitter.com/esa?ref_src=twsrc%5Etfw">@esa</a> Φ-lab:<br>- ~10,000 km² of high-res SPOT satellite imagery<br>- Multi-temporal matched low-res Sentinel2 images<br>- Stratified wrt global land-uses<br>- Enriched with sites under-represented in ML<br>🧵1/9 <a href="https://t.co/kR0AnzIlkg">pic.twitter.com/kR0AnzIlkg</a></p>&mdash; Julien Cornebise (@JCornebise) <a href="https://twitter.com/JCornebise/status/1549356696664956928?ref_src=twsrc%5Etfw">July 19, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This dataset is significant for a number of reasons:

- Greater than 100 GB of imagery with global coverage
- Covers locations typically under-represented in ML datasets
- Colocated low and high resolution imagery enables training of super resolution models
- Code provided to extend the dataset
- Models & tutorials provided
- Licenses covering non commercial use

The dataset comprises Sentinel 2 timeseries & colocated high resoluton Airbus SPOT imagery providing 10 & 1.5 m/pixel respectively. An example is shown below:

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/worldstrat/fields.jpg "Fields" )

## Getting started
I followed the instructions in the repository readme and downloaded the smaller dataset from Kaggle via the web UI. The zipped Kaggle dataset is 53GB, and even on a fast internet connection the download took 3-4 hours[^5]. I began by running the [Dataset Exploration.ipynb](https://github.com/worldstrat/worldstrat/blob/main/Dataset%20Exploration.ipynb) notebook, which gives an introduction to the dataset. Interestingly the imagery locations were suggested by several organisations:

- 22 × 22.5km² images of Amnesty provided locations or 198 × 2.5km² images.
- 39 × 22.5km² images of ASMSpotter provided locations or 351 × 2.5km² images.
- 981 × 2.5km² images of UNHCR provided locations.
- 2,407 × 2.5km² images of randomly sampled/stratified locations.

Several maps are generated using [folium](http://python-visualization.github.io/folium/) which show the capture location of the images. The image metadata is visualised in a pandas dataframe, and includes lat/lon, the source (e.g. Amnesty, UNHCR etc.) and a description field. Some very interesting locations are included, such as `Camp 25, North Korea- Gulag`, `USA - migrant camps on border` and `Brazil-Jaci_Deforestation_Cattle`. Given the provided metadata you could at this point start curating the dataset, say if you were interested in generating a version of the dataset focussed on a particular geography.

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/worldstrat/map.jpg "Example map generated in Dataset Exploration.ipynb" )

## Extending the dataset
The notebook [Dataset Generation.ipynb](https://github.com/worldstrat/worldstrat/blob/main/Dataset%20Generation.ipynb) shows how the dataset was created, and is the starting point if you want to extend the dataset yourself. To do this you can either supply a table of specific points to sample (as a csv or geojson) **or** you can uniformly sample the planet. There is an interesting dicussion on the challenges of random sampling and a mitigating strategy is provided. 

To discover available imagery you will need a SentinelHub account, and [you can get a free 30-day trial account here](https://www.sentinel-hub.com/trial). Clearly it might take some searching and good luck to locate imagery from the two satellites, over your area of interest, and within a short time window. Fortunately code is provided to assist with searching & filtering the imagery. Note that only Sentinel 2 imagery can be downloaded for free, and SPOT imagery must be purchased from Airbus. Fortunately the purchase can be performed through SentinelHub and looks pretty straightforward. Code is also provided for downloading your ordered imagery, so the whole process from discovery to ingestion of data is very well documented.

## Super resolution
One of the stated aims of releasing this dataset was to enable the training of super resolution models. The hope is that by super resolving free Sentinel imagery, researchers without the budget for purchasing high resolutuion imagery (e.g. SPOT) can use super resolved & free Sentinel imagery. Training super resolution models generally requires colocated low and high resolution imagery. One strategy often used is to downsample high resolution imagery to low resolution, and use these pairs for training. For example a 1.5m spot image could be downsampled to 10m and used to train a model that could then be applied to 10m Sentinel 2 imagery. However with this approach has disadvantages. Firstly the downsampled imagery may have different characteristics from the imagery you will use in practice, leading to unsatisfactory performance in real applications. Secondly, single imager super resolution (SISR) generally is outperformed by multi image super resolution (MISR), and creating a MISR dataset from high resoltuion imagery alone would multiply your costs significantly. Fortunately the WorldStrat dataset provides both imagery from the two satellites, and multiple frames from Sentinel 2, enabling the training of MISR super resolution models (as well as SISR). The Github code includes script for training super resolution models and an example output is shown below:

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/worldstrat/SR.jpg "Super resolution example" )

The notebook [Training.ipynb](https://github.com/worldstrat/worldstrat/blob/main/Training.ipynb) demonstrates how to run the training script. Whilst in general training is performed on a Linux machine, the authors have very helpfully included arguments if you wanted to perform training on a Windows machine. The code itself is written in python and uses pytorch and [pytorch-lightning](https://www.pytorchlightning.ai/) for the model and training loop. The code also includes logging of training metrics to [Weights & Biases](https://wandb.ai/site). The models themselves are relatively lightweight and it is suggested that training the MISR model will take 45 min - 1.5 hr on a single GPU instance. This should be within the limitations of Kaggle GPU instances so if you are interested in training the model yourself I would recommend beginning there. Note that a pretrained model is supplied in the Github repository and its use is shown in the [Inference.ipynb](https://github.com/worldstrat/worldstrat/blob/main/Inference.ipynb) notebook. If you want to read more about super resolution see the links in my satellite-image-deep-learning Github repository [here](https://github.com/robmarkcole/satellite-image-deep-learning#super-resolution). 

## Summary
Overall I am very impressed by both the size and global nature of the dataset, the quality of the documentation and code, and the level of thought that has gone into its preparation. Datasets often focus on a particular part of the world (USA mostly) and are often released without clear documentation on how they were produced, making them hard to extend.

## Footnotes
[^1]: Paper on [arXiv](https://arxiv.org/abs/2207.06418)
[^2]: Code [on Github](https://github.com/worldstrat/worldstrat)
[^3]: The full dataset is [hosted on Zenodo](https://zenodo.org/record/6810792#.YtjNb-zMK3I)
[^4]: A smaller version of the dataset [is on Kaggle](https://www.kaggle.com/datasets/jucor1/worldstrat). 
[^5]: Alternatively I could have just created a notebook on Kaggle itself, and would not have needed to wait for a download.

