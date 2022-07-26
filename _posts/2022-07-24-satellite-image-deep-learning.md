---
title: "Dissecting the satellite-image-deep-learning repo"
description: "A brief history of the popular Github repo and why you should create something similar"
layout: post
categories: [markdown]
toc: true
image: images/satellite-image-deep-learning/sat.jpg
show_image: true
hide: false
comments: true
---
## Introduction
I maintain a popular repository on Github called the satellite-image-deep-learning[^1], currently sitting close to 4k stars. The repository lists useful references I have found related to satellite imagery and deep learning, but also goes beyond this to include sections on deploying machine learning models, and even a section on 'movers and shakers' on Github. This post provides the brief history of this repository, how I find material, and why you should create something similar. A screenshot of the repository is shown below:

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/satellite-image-deep-learning/main.jpg "The repository on Github")

## History
So when and why did I start this repository? Looking at the [code-frequency](https://github.com/robmarkcole/satellite-image-deep-learning/graphs/code-frequency) chart I see I started this repository sometime in April 2018, whilst I was working at Surrey Satellites[^2]. The satellite constellation I had been hired to work on as an optical systems engineer/project manager, was on hold as it did not secure the required investment. I had demonstrated my ability to program in Python and was reassigned to assist with some development work. In particular the company had developed a basic catalogue for viewing satellite imagery & capture locations on a map, built using a single `index.html` file containing some clever Javascript, and some python scripts that processed imagery metadata into a geojson file and generated thumbnails. I was asked to add some new features after the original developer left for a role at Descartes Labs. Most of the features were quite easily implemented, such as adding new sources of archive imagery (from a pile of CD roms) and tweaking the UI by editing some Javascript. The catalogue quickly grew, and improving the search functionality became a high priority. One particular feature request was to add tags to imagery, so a user could search using terms such as `golf course` or `harbour`. Now with well geo-referenced imagery the tagging could be performed using some kind of geo-spatial lookup, but the challenge was that much of the imagery lacked precise geo-location. What options are there for tagging an aerial image like this? 

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/satellite-image-deep-learning/classification.jpg "Example of classification used to tag satellite images, taken from Kaggle")

Naturally machine learning was suggested, and I was given two days to do a POC[^3]. The time-frame was very limited so I knew I would need to hit the ground running. I was aware of convolutional neural networks and their use for classification/tagging images and began searching online for relevant articles with published code, specifically applied to satellite imagery. From memory, I recall finding many academic papers, but very few were accompanied with published code. Also for those that were published with code, the code quality could vary significantly. At this point I started making a list of good resources using Markdown[^4] in a simple README[^5] and (with permission) put this on Github. Creating a list in markdown is very straight-forward, and the basic syntax is shown below:

```
* [title](url) -> some description
```

Over time I have added more structure to the README, and added a Github action to check the validity of links, but otherwise the approach remains as simple as when I first conceived it. After leaving Surrey Satellites I moved on to other projects on Github (mostly adding extensions and integrations to Home-Assistant[^6]) but was surprised to see after a couple of years that satellite-image-deep-learning had become my most popular Github repository by star count. In Jan 2021 I joined Satellite Vu[^7] and naturally my interest in satellite imagery took center stage once more. At this point I decided to put most of my open source energy into this repository, and it has grown from strength to strength from this point onwards.

## Finding material
Many people have asked me how I find the material listed on satellite-image-deep-learning, and the answer is that for the most part it is found for me! Specifically, it is recommended in my Github feed as I have followed the right core group of developers & academics who are responsible for much of the most high profile works listed on the repository. These people also star and fork other work which is then highlighted in my feed. Since I am interested in work with published code, Github is naturally the best place to find material (honestly if it is on Gitlab I probably won't find it), but LinkedIn and Twitter are also excellent places to chance upon material. Beside these locations I also periodically check in on the Computer Vision and Pattern Recognition section of ArXiv[^8], and most days view the Remote Sensing journal[^9], screenshot below:

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/satellite-image-deep-learning/journal.jpg)

## Why you should create something similar
You might be wondering why I made the effort to create this repository, and what benefits it brings? Undeniably it is satisfying to have a popular repository on Github. It doesn't really matter to me that my most popular repository on Github doesn't contain a single line of code: it is obviously useful to at least a fraction of those that have starred it, and I feel like I have 'given back' something to the open source community to which I owe my career. I can also list several more tangible benefits:

- Kudos in the interview & hiring process
- Opens doors with other experienced developers & researchers on Github
- Receive approaches about interesting jobs & consulting opportunities
- Open source profile grants access to Github CoPilot[^10]
- Receive nice messages from people this repository has helped in their research
- Provides material to share on LinkedIn/Twitter to grow your professional network

At this point I hope I have convinced you that the barrier to entry for creating a repository like satellite-image-deep-learning is really very low. Everyone has some domain knowledge and unique areas of interest which could provide the source of inspiration for a repository like this. I actually know people who have created similar pieces of work but never shared it online since 'nobody else would be interested'. I encourage you to give it a try, as you never know where it may take you.

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/satellite-image-deep-learning/acorn.jpg "Big things have small beginnings")

## Footnotes
[^1]: https://github.com/robmarkcole/satellite-image-deep-learning
[^2]: https://www.sstl.co.uk/
[^3]: Proof of concept
[^4]: https://en.wikipedia.org/wiki/Markdown
[^5]: https://en.wikipedia.org/wiki/README
[^6]: https://www.home-assistant.io/
[^7]: https://www.satellitevu.com/
[^8]: https://arxiv.org/list/cs.CV/recent
[^9]: https://www.mdpi.com/journal/remotesensing
[^10]: https://github.com/features/copilot