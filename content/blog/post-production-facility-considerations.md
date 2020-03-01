---
title: "Post-production facility considerations"
date: 2019-12-26T19:52:15Z
tags: [ 'post-production']
draft: false
---

Key points when considering to build a post-production facility:

- **Designing system for the entire facility**: _What is the medium & viewing target of the provided services_?     
    
    The answer to this question determines the kind of system a facility needs.    
    As a general rule of thumb if a facility needs to facilitate the top two kinds [^note] of the production types , then we will be talking about medium to large facility. Technical specifications includes but not limited to: 
    - storing at least 6 months worth of data (safe to say 40-50TB is the least amount of storage capacities for 3-8 people)
    - internal network capable of serving real-time video (_emphasis in visual because audio is much lighter_) data to workstations
    - multiple specific (often turn-key) hardwares & softwares for handling the workloads for finishing to media format(s) on those workstations as the project requires, usually in multiple versions. 

    There are other specification details involved in the working environments that needs to be done properly as well to make sure the end results will be matching industry standards expectation, a few examples are electrical, lighting, and even color management detail like neutral color paint for walls inside the working area. 

- **Finalising based on type of services and amount of people in the entire team**: _What specific parts of post-production the company caters, and how many people work on each of these parts_?     

    There are several stages in post-production: story editing, color correction, finishing, and mastering. In visual post-production, sound is involved in most of the stages but not as much as in audio post-production company, this allows the production team to split and worked in parallel if necessary.    
    Story editing stage usually only requires modest hardware requirements compared to later stages because its main purpose is basically finalising the story from draft to final version. Therefore at this stage there is no real need to work directly with the original footage data, most of the time the common strategies for selecting & cutting footages involve proxy files or smaller transcoded files.      
    Color correction or grading, as well as finishing stage, constitute the bulk in hardwares & software requirements [^bandwidth] because of file size, bandwidth and processing power needed to process those files.      
    Finishing consists of many components like motion graphic, compositing, VFX, 3D VFX, etc, and in the case of movie production, color grading and subtitling or closed captioning.         
    Mastering, depending on what kind of formats, can be an independent system on its own. In celluloid era mastering often means an entire separate facility.
         
    Workflows, structures and pipelines are entirely dependent on these parts. 
    
> Please note that _data lineage_ and _integrity_ are **crucial** in every stages. From the time the shoot started until deliverables has been delivered and backed up, every relevant data and metadata _should be present and preserved_. Centralized storage server(s) will mostly be needed when dealing with more than 3 workstations. 


 
[^note]: **Production types**

    - **_Film production_**: A film or digital movie theatre is projection based, so the entire production pipeline needs to be aligned to its requirements, to ensure the end result of post production (deliverables) are suited for their venue viewings. Practically this means movies have to be prepared, shot, edited & finished for projections, TVs, _and_ other screen based viewings as well. Standard deliverables usually are digital masters for theaters, teasers/trailers/promos for TV stations or networks, and then to online distributions; all having distinct and overlapping sets of requirements.     
    These are the reasons why feature length motion pictures takes a lot more compared to other projects; starting from duration, amount of processing, to level of industry knowledge for achieving picture & sound quality. Overall movie projects usually involve much higher complexity compared to the others. Since mid to late 2000s the global movie industry had rapidly moved to digital based medium (DHCP format) from film (celluloid), and along with Internet, the demand for technology level in post-production arose sharply as well.
    
    - **_TV based production_**: (HD)TV based production that produces advertisements/commercials, or other motion picture such as straight to home movie like HBO or movie in medium such as BluRay, they need to adhere to well-established broadcasting standards within the relevant distribution region in order to be accepted by broadcasting station systems and home viewing systems. Usually the main component of technical problems in this production revolves around time constraint.
    
    - **_Online video_**: Either Vimeo, Youtube or other online video platforms, this type of production is essentially almost the same as TV based production, just lacking in stricter (technical) requirements due to the wild west nature of internet especially when the context is consumer's side. Highest quality can be achieved by following the majority of standard practices followed in film or TV based production.     
    One particular exception here is Netflix. Although Apple's iTunes requirements also demands higher standards than let's say Youtube, Netflix more or less has the same requirement as film production, especially with regard to HDR production/deliverables. They published and maintained an up-to-date list of technical requirements for their partners within their site, covering almost every aspects in Production and Post Production.


[^bandwidth]: **Technical references**      
    A few bandwidth requirements for common RAW files in digital cinema cameras          
    * R3D : https://www.red.com/recording-time   
    * ARRIRAW : https://tools.arri.com/fileadmin/adapps/afdc/AFDC.html
