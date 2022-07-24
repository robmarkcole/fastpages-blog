---
title: "Dissecting the satellite-image-deep-learning repo"
description: "How I maintain the popular Github repo and why you should create something similar"
layout: post
categories: [markdown]
toc: true
image: images/satellite-image-deep-learning/sat.jpg
show_image: true
hide: false
---
## Introduction
I maintain a popular repository on Github called the satellite-image-deep-learning[^1], currently sitting close to 4k stars. The repository basically lists useful references I have found related to satellite imagery and deep learning, but also goes beyond this to include sections on deploying machine learning models, and even a secton on 'movers and shakers' on Github. This post provides the background to this repository, how I maintain & develop it, and why you should create something similar. A screenshot of the repository is shown below:

![](https://raw.githubusercontent.com/robmarkcole/blog/master/images/satellite-image-deep-learning/main.jpg "The repository on Github")

## History
So when and why did I start this repository? Looking at the [code-frequency](https://github.com/robmarkcole/satellite-image-deep-learning/graphs/code-frequency) chart I see I started this repository sometime in early 2018, whilst I was working at Surrey Sattelites[^2]. The satellite constellation I had been hired to work on as an optical systems engineer/project manager, was on hold as it did not secure the required investment. I had demonstrated my ability to program in python and was reassigned to assist with some development work. In particular the company had developed a basic catalogue for viewing satellite imagery & capture locations on a map, built using folium[^3] and some python scripts. I was aksed to add some new features after the primary maintainer left for a role as Descartes Labs. Most of the features were quite easily implemented, such as adding new sources of archive imagery (from a pile of CD roms) and tweaking the UI with some Javascript. The catalogue quickly grew and improving the search functionality became a high priority. One particular request was to add tags to imagery, so a user could search using terms such as `residential area` or `port`. Now with well georeferenced imagery the tagging could be performed using some kind of geospatial lookup, but the challenge was that much of the imagery lacked precise geolocation. What options are there for tagging an aerial image like this? 

Naturally machine learning was suggested, and I was given two days to do a POC[^4]. The timeframe was very limited so I knew I would need to hit the ground running. I was aware of CNNs and their use for classification/tagging images and began searching online for relevant articles with published code, specifically applied to satellite imagery. From memory, I recall finding many academic papers, but very few were accompanied with published code. Also for those that were published with code, the code quality could vary significantly. At this point I started making a list of good resources using Markdown[^5] in a simple README[^6] and (with permission) put this on Github. Creating an list in markdown is very straight-forward, and the basic syntax is shown below:

```
* [title](url) -> some description
```

Over time I have added more structure to the README, and added a Github action to check the validity of links, but otherwise the approach remains as simple as when I first conceived it. After leaving SSTL I moved on to other projects on Github (mostly adding extensions and integrations to Home-Assistant[^7]) but was suprised to see after a couple of years that satellite-image-deep-learning had become my most popular work by star count. In Jan 2021 I joined Satellite Vu[^8] and naturally my interest in satellite imagery took center stage once more. At this point I decided to put most of my open source enrgy into this repository, and it has grown from strenght to strength from this point onwards.


## Summary
A low overhead reposotiroy can help you build your reputation on Github and grow your professional network. 

## Footnotes
[^1]: https://github.com/robmarkcole/satellite-image-deep-learning
[^2]: https://www.sstl.co.uk/
[^3]: http://python-visualization.github.io/folium/
[^4]: Proof of concept
[^5]: https://en.wikipedia.org/wiki/Markdown
[^6]: https://en.wikipedia.org/wiki/README
[^7]: https://www.home-assistant.io/
[^8]: https://www.satellitevu.com/