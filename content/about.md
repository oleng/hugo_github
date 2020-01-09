---
title: "about"
date: 2019-12-26T19:52:15Z
draft: false
---

> ##### `$ whoami` 
> I was a Digital Imaging Technician (DIT) for a motion picture production company, became a Post-Production engineer slash Post-Production supervisor since end of 2009. 
> Now I'm looking for work opportunities in software engineering fields, particularly in **DevOps** and **Data Engineering**.    
> 
> Tools
> : _Python, Bash, SQLite, Redis, PostgreSQL, Docker, macOS, Ubuntu_      
>
> To do
> : _Go, Rust, Kubernetes, Kafka, Graph databases, Hashi Vault, Prefetch, Argo_  
> 
> If you're interested in reaching me for work opportunities:    
> [ ![emailme](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABkAAAAZCAYAAADE6YVjAAABC0lEQVRIx+3Uu0oDQRgF4C8i0cdQUCwUbCzUh7AQBFsLy/gEgtj4ADGlLyA2lmKllbWgjVVUjMHC2iwhazPFEpLZzQUs3ANTzH85Z4bzz1CiRIn/g8qQ+Hwkl4cUP3ki26ihGhpGPXSCOh5ihR+BfJL1nneTdNpWzAxIHqA1AXk7cIiJtLCHmzEEbkPvZ17hF06wglN0C3jQwxmWcRw4ckcwwTWWsIPXiEAbu1jEJTpFfM0SPGMT67jru1UX99jAFh77eguLpPjGEVbRwEtYjRCrhZp0mEjREU5whYtMTw+HwehqbIRHeScpmngK+zUsRL6fyp8/xrcpCDSzm9kBBfvBzLkxP8gOzrPBX2pNZi4bjaDaAAAAAElFTkSuQmCC)](mailto:tjioechandra.official@gmail.com) ⠀<tjioechandra.official@gmail.com>     
> [![Linkedin](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABYAAAAWCAYAAADEtGw7AAAAQXRFWHRDb21tZW50AENSRUFUT1I6IGdkLWpwZWcgdjEuMCAodXNpbmcgSUpHIEpQRUcgdjYyKSwgcXVhbGl0eSA9IDkwCrBFWJMAAAIwSURBVDjL1dU/iBVXFMfxz7y3Khu8YNYEzWgTxQR1IaBFQASFgFiIkhCIKBYRC0tRLAXBpBYsUqSwScAmBBuLQApRCIpYhcjGBCwMRyEqyl3FP7s7ae6DcfJ291l64DB/7pzvzLnnd87wtlk1ykN1Xfcxhl4rZg6zmImI5o3AdV0vw0ocwh5swTtl+R9cxQ+4EREPRgLXdT2BIziGDxZJ6ld8i98i4iX054F+iG9wEqmk3czjFdZhBx6nlKZyzjP9IdBxnMbh1our4k3rvO3wLibxV875dr8D7eEgTmFJCfobX2MD1swDHdgE3k8pXXsNnFIaw3msbZpmtqqqHr6MiF9SSg/w1QgiWoffu+C9OFqkNVtVVR/jKaU/SiE/WQQ6N9iysc7CTixr7essduOzsjXPi8wSXiBjHGuxtOgcPu11wJs6132ciYj3cBxT+Bj7sDUiJiNiPX7qxK3qglcMSa/fOvYiYg638EVd1/vK2kU8aQd1wXmRtm+Kcj7Hdzhe1/Vy3MX0QuDbI1R9DKuLppWaPCv1GNijLvgKXo0An2uBm5bmB3ajC76IO517zZDrZsh6G3ypq+NBy+4qGobplNIEtmMjnpa5sBEz5eu3YluR3nWcq4bMiuX4HvtHndctu4cTEXHhf0Mo5/wypTRVRL+hFHih6TbI8j7O4kLO+cXQsZlz/jeldK1o96My3KsF/GaZiD9GxPQof5BUuvFAaffNrYZ5WIA/43JE/NmO/Q9BlqNNOdfmZwAAAABJRU5ErkJggg==)](https://www.linkedin.com/in/tjioe-oleng-chandra) ⠀[linkedin](https://www.linkedin.com/in/tjioe-oleng-chandra/) 

I used to be a person who build facility for visual post-production companies in Jakarta. I've **designed**, **budgeted**, **purchased**, **built** and **maintained** a few of them. In general this involves:

- **Designing system for the entire facility**: _What is the medium & viewing target that company provides services for_?     
    
    The answer to this question determines the kind of system a facility needs.    
    As a general rule of thumb if a facility needs to facilitate the top two kinds of the production types [^note], then we'll be talking about medium to large facility. Technical specifications including but not limited to: 
    - storing at least 6 months worth of data (safe to say 40-50TB is the least amount of storage capacities for 3-8 people)
    - internal network capable of serving real-time those video (_emphasis in visual because audio is much lighter_) data to workstations
    - multiple specific hardwares & softwares for handling those workstations loads for finishing to media format(s) the project requires, usually in multiple versions. 

    There are other specification details involved in the working environments needed to be done properly as well to make sure the end results will be matching industry standards expectation. 
    I have been directly involved in several Indonesian movies, and most of the companies I worked with were doing TV commercials on daily basis. 

- **Finalising based on type of services and amount of people in the entire team**: _What specific parts of post-production the company caters, and how many people work on each of these parts_?     

    There are several stages in post-production, mainly story editing, color correction, finishing, and mastering. In visual post-production, sound is involved in most of the stages but not as much as in audio post-production company, this allows the production team to worked in separate if necessary.    
    Story editing stage usually only requires modest hardware requirements compared to the others in later stages because its main purpose is basically finalising the story from draft to final version.    
    Color correction or grading, as well as finishing stage of post-production form the bulk in hardwares & software requirements.      
    Finishing consists of many components like motion graphic, compositing, VFX, 3D VFX, etc, and in the case of movie production, color grading.         
    Mastering, depending on what kind of format, can be an independent system on its own. In celluloid era mastering often means an entire separate facility.
         
    Workflows, structures and pipelines are entirely dependent on these parts. Centralized storage server(s) will often be needed when dealing with more than 3 workstations. 

 
 
 
[^note]: **Production types**

    - **_Film production_**: A film or digital movie theatre is projection based, so the entire production pipeline needs to be aligned to its requirements, to ensure the end results of post production (deliverables) are suited for their venue viewings, not excluding TVs and screen based devices for trailers & promos. This usually has the heaviest requirements from all projects, due to duration, processing & industry knowledge for preserving picture quality, and higher complexity in general. Since mid to late 2000s the global movie industry had rapidly moved to digital based medium (DHCP format) from film (celluloid). One particular note, Netflix has more or less the same requirement as film production.
    
    - **_TV based production_**: TV based production companies that produces advertisements/commercials, or other motion picture such as home movie in medium such as BluRay, need to adhere to well established broadcasting standards in order to be accepted by broadcasting station systems, usually the main component of technical problems in this production is time constraint.
    
    - **_Online video_**: Either Vimeo or Youtube, this type of production is essentially almost the same as TV based production, they only lacking stricter (technical) requirements due to the wild west nature of internet. Highest quality can be achieved by following the majority of standard practices followed in film or TV based production. 
