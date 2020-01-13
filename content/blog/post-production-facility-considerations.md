---
title: "Post-production facility considerations"
date: 2019-12-26T19:52:15Z
tags: [ 'post-production']
draft: false
---

Key points when considering to build a post-production facility:

- **Designing system for the entire facility**: _What is the medium & viewing target that company provides services for_?     
    
    The answer to this question determines the kind of system a facility needs.    
    As a general rule of thumb if a facility needs to facilitate the top two kinds of the production types [^note], then we'll be talking about medium to large facility. Technical specifications including but not limited to: 
    - storing at least 6 months worth of data (safe to say 40-50TB is the least amount of storage capacities for 3-8 people)
    - internal network capable of serving those real-time video (_emphasis in visual because audio is much lighter_) data to workstations
    - multiple specific hardwares & softwares for handling those workstations loads for finishing to media format(s) the project requires, usually in multiple versions. 

    There are other specification details involved in the working environments needed to be done properly as well to make sure the end results will be matching industry standards expectation. 

- **Finalising based on type of services and amount of people in the entire team**: _What specific parts of post-production the company caters, and how many people work on each of these parts_?     

    There are several stages in post-production, mainly story editing, color correction, finishing, and mastering. In visual post-production, sound is involved in most of the stages but not as much as in audio post-production company, this allows the production team to worked in separate if necessary.    
    Story editing stage usually only requires modest hardware requirements compared to the others in later stages because its main purpose is basically finalising the story from draft to final version. So at this stage there's no real need to work directly with the original footage data, most of the time the strategies for selecting & cutting footages involves proxy files or smaller transcoded files.    
    Color correction or grading, as well as finishing stage of post-production form the bulk in hardwares & software requirements[^bandwidth] because of the file size, bandwidth and processing power needed to process those files.      
    Finishing consists of many components like motion graphic, compositing, VFX, 3D VFX, etc, and in the case of movie production, color grading.         
    Mastering, depending on what kind of formats, can be an independent system on its own. In celluloid era mastering often means an entire separate facility.
         
    Workflows, structures and pipelines are entirely dependent on these parts. Centralized storage server(s) mostly will be needed when dealing with more than 3 workstations. 


 
[^note]: **Production types**

    - **_Film production_**: A film or digital movie theatre is projection based, so the entire production pipeline needs to be aligned to its requirements, to ensure the end result of post production (deliverables) are suited for their venue viewings. Practically this means movies have to be prepared, shot, edited & finished for projections, TVs, _and_ other screen based viewings as well. Standard deliverables usually are digital masters for theaters, teasers/trailers/promos for TV stations/networks, and then online distributions; all having distinct and overlapping sets of requirements.     
    These are why feature length motion pictures takes a lot more compared to other projects; starting from duration, amount of processing, to level of industry knowledge for achieving picture & sound quality, overall movie projects involve much higher complexity compared to the others. Since mid to late 2000s the global movie industry had rapidly moved to digital based medium (DHCP format) from film (celluloid), and along with Internet, the demand for technology level in post-production arose sharply as well. One particular note, Netflix has more or less the same requirement as film production, especially with regard to HDR production/deliverables.
    
    - **_TV based production_**: (HD)TV based production that produces advertisements/commercials, or other motion picture such as straight to home movie like HBO or medium such as BluRay, they need to adhere to well established broadcasting standards in order to be accepted by broadcasting station systems and home viewing systems. Usually the main component of technical problems in this production is involving time constraint.
    
    - **_Online video_**: Either Vimeo, Youtube or other online video platforms, this type of production is essentially almost the same as TV based production, only lacking in stricter (technical) requirements due to the wild west nature of internet especially when the context is consumer's side. Highest quality can be achieved by following the majority of standard practices followed in film or TV based production, which happens to be the requirement standard picked by major online distributors like iTunes and (especially) Netflix. 

[^bandwidth]: Bandwidth requirements for digital cinema RAW cameras          
    - R3D : https://www.red.com/recording-time   
    - ARRIRAW : https://tools.arri.com/fileadmin/adapps/afdc/AFDC.html
