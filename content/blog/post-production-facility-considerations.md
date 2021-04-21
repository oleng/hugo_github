---
title: 'Post-production facility considerations'
date: 2019-12-26T19:52:15Z
tags: [ 'post-production' ]
draft: false
---

In this post I'd like to provide a few key points as guide to determine the technical aspects of a post-production facility based on my past experience in building a small boutique facility, but should be applicable to medium size as well. Most of the companies I worked with were working on TV commercials on daily basis, with the majority of them shot on digital cinematography cameras such as RED, ARRI Alexa, or high speed cameras like Phantom. I was also directly involved in several movie titles, such as [Bebek Belur](https://www.imdb.com/title/tt1631681/) 2010, [Garuda di Dadaku 2](https://www.imdb.com/title/tt1987569/) 2011 (shot on celluloid)) , [Langit Ke-7](https://www.imdb.com/title/tt7601390/) 2012, and [The Raid 2: Berandal](https://www.imdb.com/title/tt2265171/) 2014.      

Here are some initial questions that help you determine the kind of system and tech stack that a facility needs.

## Designing system for the entire facility
#### _What is the medium & viewing target of the provided services?_

As a general rule of thumb if a facility needs to facilitate the top two kinds [^note] of the production types, then we will be talking about medium to large facility. Technical specifications includes but not limited to:
- The maximum requirement to meet, for instance if the facility is to provide service for processing 8K 3D/stereoscopic IMAX footages, the amount of data traffic that you need to consider greatly differs to a facility that only needs to deal with 1080p footages.
- storing at least 6 months worth of data (safe to say 40-50TB is the least amount of storage capacities for 3-8 people)
- internal network capable of serving real-time video (_emphasis in visual because audio is much lighter_) data to workstations
- multiple specific (often turn-key) hardwares & softwares for handling the workloads for finishing to media format(s) on those workstations as the project requires, usually in multiple versions.

There are other specification details involved in the working environments that also needs to be done properly to make sure the end results will be matching industry standards expectation.
A few examples are electrical, lighting, and even color management detail like neutral color paint for walls inside the working area.


## Finalising based on type of services and amount of people in the entire team
#### _What specific parts of post-production the company caters, and how many people work on each of these parts?_

There are several stages in post-production: story editing, color correction, finishing, and mastering. In visual post-production, audio is still involved in most of the stages but not as much as in audio post-production company, this separation allows the production team to split so they can work on both visual and audio in parallel if necessary. Traditionally finalizing audio mastering is done after pictures are locked in visual post.    

Story editing stage usually only requires modest hardware requirements compared to later stages because its main purpose is basically just finalising the story from draft to final version. Therefore at this stage there is no real need to work directly with the original footage data, and most of the time the common strategies for selecting & cutting footages involve proxy files or smaller transcoded files.    

Color correction or grading, as well as finishing stage, constitute the bulk in hardwares & software requirements [^bandwidth] because of the amount of data, bandwidth and processing power needed to process those files.    

Finishing consists of many components like motion graphic, compositing, VFX, 3D VFX, etc. In the case of movie production, color grading and subtitling or closed captioning.        

Mastering, depending on what kind of formats, can be an independent system on its own. In celluloid era mastering often means an entire separate facility.

&nbsp;

> The answers to these questions will serve as guide to design workflows, structures, pipelines, and specifications you need to build. Centralised storage server(s) will most likely be needed when dealing with more than 3 workstations.

> Please note that _data lineage_ and _integrity_ are **crucial** in every stages. From the time the shoot started, every relevant data and metadata _should be present, preserved, and backed up_ in order to have an optimised, high performing teams and workflows. Coordination with DITs or post production supervisor is very important to avoid problems further along the production pipeline.    



[^note]: **Production types**

    - **_Film production_**: A film or digital movie theatre is projection based, so the entire production pipeline needs to be aligned to its requirements, to ensure the end result of post production (deliverables) are suited to the requirement standards from these venues. Practically, this means movies have to be prepared, shot, edited, and finished for several mediums: projections, TVs, _and_ other screen based viewings. Standard deliverables usually are digital masters for theaters, teasers/trailers/promos for TV stations/networks, and for online distributions; all having distinct and overlapping sets of requirements.    
    These are the reasons why feature length motion pictures involve much higher complexity compared to other projects; starting from duration, amount of processing, to level of industry knowledge on achieving picture & sound quality.    
    Since mid to late 2000s the global movie industry had rapidly moved to digital medium (DCP) from film (celluloid), and along with Internet, the demand for technology level in post-production arose sharply as well.

    - **_TV based production_**: (HD/UHD)TV based production that produces advertisements/commercials, or other motion picture such as straight to home movie like HBO or in medium such as BluRay, they need to adhere to well-established broadcasting standards within the relevant distribution region in order to be accepted by broadcasting station systems and home viewing systems. Usually the main component of technical problems in this production revolves around time constraint.

    - **_Online video_**: Either Vimeo, Youtube or other online video platforms, this type of production is essentially almost the same as TV based production, just lacking in stricter (technical) requirements due to the wild west nature of internet especially when the context is consumer's side. Highest quality can be achieved by following the majority of standard practices followed in film or TV based production.    
    _One particular exception here_ is **Netflix**. Although Apple's iTunes requirements also demands higher standards than let's say Youtube, Netflix more or less has the same requirement as film production, especially with regard to HDR production/deliverables. They published and maintained an up-to-date list of technical requirements for their partners within their site, covering almost every aspects in Production and Post Production.


[^bandwidth]: **Technical references**
    A few bandwidth requirements for common RAW files in digital cinema cameras
    * R3D : https://www.red.com/recording-time
    * ARRIRAW : https://tools.arri.com/fileadmin/adapps/afdc/AFDC.html
