---
title: "Quick tour of the WorldStrat Dataset"
description: "This significant new dataset raises the bar for documentation quality"
layout: post
categories: [markdown]
toc: true
image: images/worldstrat/main.jpg
show_image: true
hide: true
comments: true
---

## Introduction
A new dataset called the WorldStrat dataset was recently announced on Twitter by [Julien Cornebise](https://twitter.com/JCornebise), [Ivan Orsolic](https://twitter.com/ivanorsolic), and [Freddie Kalaitzis](https://twitter.com/alkalait). The dataset raises the bar in documentation quality of a dataset and the release includes a paper on arXiv[^1], code on Github[^2], and the dataset itself on both Zenodo[^3] and Kaggle[^4]. 

<blockquote class="twitter-tweet tw-align-center"><p lang="en" dir="ltr">Proud to release the WorldStrat dataset with <a href="https://twitter.com/ivanorsolic?ref_src=twsrc%5Etfw">@ivanorsolic</a> <a href="https://twitter.com/alkalait?ref_src=twsrc%5Etfw">@alkalait</a> and <a href="https://twitter.com/esa?ref_src=twsrc%5Etfw">@esa</a> Φ-lab:<br>- ~10,000 km² of high-res SPOT satellite imagery<br>- Multi-temporal matched low-res Sentinel2 images<br>- Stratified wrt global land-uses<br>- Enriched with sites under-represented in ML<br>🧵1/9 <a href="https://t.co/kR0AnzIlkg">pic.twitter.com/kR0AnzIlkg</a></p>&mdash; Julien Cornebise (@JCornebise) <a href="https://twitter.com/JCornebise/status/1549356696664956928?ref_src=twsrc%5Etfw">July 19, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This dataset is significant for a number of reasons:

- Greater than 100 GB of imagery with global coverage
- Covers locations typically under-represented in ML datasets
- Colocated low and high resolution imagery
- Code provided to extend the dataset & integrate with the EO-Learn[^5] Python package
- Models & tutorials provided
- Demonstrates super resolving Sentinel 2 imagery
- The code, the Sentinel 2 images, the locations, the methodology, and the pre-trained models are all licensed for commercial use (SPOT imagery is NOT)

The dataset comprises Sentinel 2 time-series & colocated high resoluton Airbus SPOT imagery providing 10 & 1.5 m/pixel respectively. An example is shown below:

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/worldstrat/fields.jpg "Fields" )

## Getting started
I followed the instructions in the repository readme and downloaded the smaller dataset from Kaggle via the web UI. The zipped Kaggle dataset is 53GB, and even on a fast internet connection the download took 3-4 hours[^6]. I began by running the [Dataset Exploration.ipynb](https://github.com/worldstrat/worldstrat/blob/main/Dataset%20Exploration.ipynb) notebook, which gives an introduction to the dataset. Interestingly the imagery locations were suggested by several organisations:

- 22 × 22.5km² images of Amnesty provided locations or 198 × 2.5km² images.
- 39 × 22.5km² images of ASMSpotter provided locations or 351 × 2.5km² images.
- 981 × 2.5km² images of UNHCR provided locations.
- 2,407 × 2.5km² images of stratified-sampled locations to ensure coverage of all types of land-use and human density

Several maps are generated using [folium](http://python-visualization.github.io/folium/) which show the capture location of the images. The image metadata is visualised in a pandas dataframe, and includes lat/lon, the source (e.g. Amnesty, UNHCR etc.) and a description field. Some very interesting locations are included, such as `Camp 25, North Korea- Gulag`, `USA - migrant camps on border` and `Brazil-Jaci_Deforestation_Cattle`. Given the provided metadata you could at this point start curating the dataset, say if you were interested in generating a version of the dataset focussed on a particular geography.

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/worldstrat/map.jpg "Example map generated in Dataset Exploration.ipynb" )

## Extending the dataset
The notebook [Dataset Generation.ipynb](https://github.com/worldstrat/worldstrat/blob/main/Dataset%20Generation.ipynb) shows how the dataset was created, and is the starting point if you want to extend the dataset yourself. To do this you can either supply a table of specific points to sample (as a csv or geojson) **or** you can uniformly sample the planet. There is an interesting dicussion on the challenges of random sampling and a mitigating strategy is provided. To discover available imagery you will need a SentinelHub account, and [you can get a free 30-day trial account here](https://www.sentinel-hub.com/trial). Clearly it might take some searching and good luck to locate imagery from the two satellites, over your area of interest, and within a short time window. Fortunately code is provided to assist with searching & filtering the imagery. Note that only Sentinel 2 imagery can be downloaded for free, and SPOT imagery must be purchased from Airbus. Fortunately the purchase can be performed through SentinelHub and looks pretty straightforward. Code is also provided for downloading your ordered imagery, so the whole process from discovery to ingestion of data is very well documented.

## Super resolution
One of the stated aims of releasing this dataset was to enable the training of super resolution models. The hope is that by super resolving free Sentinel imagery, users without the budget for purchasing high resolution imagery (e.g. SPOT) can use super resolved & free Sentinel imagery in their applications. Training super resolution models generally requires colocated low and high resolution imagery, and to this end the WorldStrat dataset provides both low and high resolution imagery. Multiple low resolution frames from Sentinel 2 are provided for each location, enabling the training of multi-image super resolution models, as well as the more typical single-image super resolution models. The Github code includes a script for training super resolution models and an example output is shown below:

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/worldstrat/SR.jpg "Super resolution example" )

The notebook [Training.ipynb](https://github.com/worldstrat/worldstrat/blob/main/Training.ipynb) demonstrates how to run the training script. Whilst in general training is performed on a Linux machine, the authors have very helpfully included arguments if you wanted to perform training on a Windows machine. The code itself is written in python and uses pytorch and [pytorch-lightning](https://www.pytorchlightning.ai/) for the model and training loop. The code also includes logging of training metrics to [Weights & Biases](https://wandb.ai/site). The models themselves are relatively lightweight and it is suggested that training the multi-image super resolution model will take 45 min - 1.5 hr on a single GPU instance. This should be within the limitations of a Kaggle GPU instance, so if you are interested in training the model yourself I would recommend beginning there. Note that a pretrained model is supplied in the Github repository and its use is shown in the [Inference.ipynb](https://github.com/worldstrat/worldstrat/blob/main/Inference.ipynb) notebook. If you want to read more about super resolution read section 4.1 of the ArXiv paper and see the links in my satellite-image-deep-learning Github repository [here](https://github.com/robmarkcole/satellite-image-deep-learning#super-resolution).

## Other uses for the dataset
The availability of high resolution imagery is of significant interest in itself, since this is typically very expensive to acquire. This dataset covers locations typically under-represented in high resolution datasets and so will be of significant interest to those who study those locations. All images in this dataset are provided without annotation, so their use in applications such as segmentation or object detection would first require annotation to be performed[^7]. In the ArXiv paper they note: 'Because every image is geo-referenced and timestamped, it is also possible to cross-reference it with any other source of label, for example mapping databases like OpenStreetMap, for building imprints, structure detection, etc'. However there are a number of unsupervised or self-supervised techniques which do not required annotated data. In particular self supervised change detection is a technique that can be performed on the Sentinel 2 time series imagery, and where having the high resolution reference could aid with evaluation of predictions. A good introductory read on this topic is the paper [Self-supervised Remote Sensing Images Change Detection at Pixel-level](https://arxiv.org/abs/2105.08501v2)

## Datasheet
The appendix of the ArXiv paper includes a `Datasheet` for the dataset which describes the motivation, composition, collection process & recommended uses for the dataset following a methodology presented in the paper Datasheets for Datasets[^7]. The purpose of including this datasheet is to improve & standardise the quality of the documentation, in order to enable the use of the dataset with confidence and provide transparency and accountability around the production of the dataset itself. I think this is a very welcome inclusion and I hope to see more datasets published with an accompanying Datasheet.

## Summary
Overall I am very impressed by both the size and global nature of the dataset, and the high quality of the documentation and code. Datasets often focus on a particular part of the world (USA mostly) and are often released without clear documentation on how they were produced, making them hard to extend or use with confidence. Therefore WorldStrat demonstrates best practice for publishing a dataset which I hope other publishers will emulate. Sentinel 2 imagery is widely used and so enhancement of its qualities through applications such as super resolution could have significant positive impact on end users. Finally I would like to thank Julien Cornebise for his feedback on the draft of this post.

## Footnotes
[^1]: https://arxiv.org/abs/2207.06418
[^2]: https://github.com/worldstrat/worldstrat
[^3]: https://zenodo.org/record/6810792#.YtjNb-zMK3I
[^4]: https://www.kaggle.com/datasets/jucor1/worldstrat
[^5]: https://eo-learn.readthedocs.io/en/latest/index.html
[^6]: Alternatively I could have just created a notebook on Kaggle itself, and would not have needed to wait for a download
[^7]: https://arxiv.org/abs/1803.09010

