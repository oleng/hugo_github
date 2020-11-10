---
title: "Google's official API client libraries explained"      
date: 2020-11-09T16:23:40Z     
tags: [ 'development','python' ]       
draft: false    
---

The purpose of this short explanation is an attempt for a brain dump, to maintain 
bookmarks of relevant links that reflects most current state of Google's Python 
client libraries for their services, as they have somewhat complex to navigate 
sites for official libraries. Not as unusable as Microsoft or several other 
dinosaur companies, but enough to waste non trivial amount of time.

Figuring out their ins & out haven't been fun, I found re-learning is even less fun. 
I immensely dislike having to browse and read pages full of vague lingos just to 
figure out vague Java method procedures that they're using as backend. Thus this post.

This also serves as a rant post, at time with profanities, since I think they 
didn't care to actually give developers enjoyable experience in client library matters. 
I've encountered period of limbo, around 2017 to early 2019, where few of 
their client libraries were stuck in a state of deprecation without clear direction 
on what that means for users.         
It might not sounds like a big deal, except I found this out because I needed 
their [OAuth library](https://oauth2client.readthedocs.io/), a key point into 
their services. The informations I could found were conflicting each other, 
there was more than one third party libraries built to fill the gap that OAuth and
Google created with their lack of clarity and was confusing af at some point because
links formed circular loop. It cost me days of sorting out informations from guides
and the documentation sites. I ended up using `requests-oauthlib`.

They're also infamous for killing products _and_ changing brands, and it seems to me 
they only started to make an effort for streamlined, unified libraries & documentations 
in recent few years (at least for Python libraries), as there are still some old 
tutorials & guides on their pages that are not updated yet, which can mislead users.

##### Overview

At the risk of oversimplifying their product line (I'm totally fine with that),
basically they have two suites for two levels of users/client, Google Cloud and G Suite.

Google Cloud is a product suite for their Cloud services, few has free tier
offering, but most are geared for enterprise billing customers.        
Their product page is https://cloud.google.com/, and their web based management UI is
located at https://console.cloud.google.com/

On lower tier they have Google Workspace (formerly G Suite), it's a paid product suite
for small-medium offices, but most are available for free with better limits than Cloud ones.         
The official page is at https://workspace.google.com, with web based UI management in
  https://admin.google.com

Most of the individual product in G Suite supports API access through their client library, 
but for basic users a.k.a non paying clients, seems like there's no way to have 
a central, codeless admin dashboard to orchestrate or administrate, so these type of 
users have to go through individual documentation for each library.

Complete list to their products for developers can be found in
  https://developers.google.com/products/develop

&nbsp;&nbsp;&nbsp;&nbsp;

Below are the relevant Python libraries.

------

##### Google Auth Python library

I'm not a fan of sending out API keys embedded in url requests like from `curl` or any other
methods, so OAuth is essential for avoiding that, as well as future proofing identification 
procedure for any API activities inside any apps.

It turns out that there's somewhat ambiguous URI for developer console related with authentication API at https://console.developers.google.com/, I'm sure this detail has escaped me entirely before.     
It's the same dashboard for cloud services administration, only with limited features and different title (`Google APIs` instead of `Google Cloud Platform`).

![Google APIs dashboard](https://oleng.github.io/static/img/googleapis_dashboard.png) ![Google Cloud Platform dashboard](https://oleng.github.io/static/img/googlecloudplatform_dashboard.png) 

 AFAIK there's no attempt to explain the real difference between the two, other than the obvious conclusion that one discerns after the fact of learning that there are two dashboards, and the titled Cloud Platform is for enterprise customers. It's probably clear and normal to some people but I find it not very user friendly to have different entry points without any clear patterns or context, it's a little disorienting. I can access them both as lowly normal user, so why not just consolidate them in one place.

Packages:    
  
- `google-auth` - see https://pypi.org/project/google-auth for latest version.      
- `google-auth-oauthlib` - see https://pypi.org/project/google-auth-oauthlib for latest version.

URLs:

_Repository_       
  https://github.com/googleapis/google-auth-library-python      
  https://github.com/googleapis/google-auth-library-python-oauthlib     
  [narrator] : _very user friendly, aren't they?_
  
_Documentation_       
  https://googleapis.dev/python/google-auth/latest  

Note:      
  Support async
  
------

##### Google Suite client libraries

1. **Google API Python library**

    Honestly I had no fucking idea what exactly this is for/why it exists, 
    I was guessing it's either to be used in conjuction with the real libraries or to force
    people to directly interacting with API endpoints. 
    
    The docs homepage only offered this explanation     

    > The Google API Client Library for Python is designed for Python client-application developers. It offers simple, flexible access to many Google APIs.

    with these TOC guides     

    > * Getting started 
    > * Auth ...
    > * How to…    
    >   * Use Logging     
    >   * Upload Media    
    >   * Use Mocks    
    > ...etc
    
    But if you go to Google APIs organization page in Github and search for
    individual products' Python client library, you won't find it. 
    So it seemed to me that my second guess is what Google wanted from developers,
    and from the surface it looked like my suspicion is confirmed by their [sample code used
    for guides](https://developers.google.com/drive/api/v3/quickstart/python).
    They have this `discovery` module to somehow `build` services.
    
    Packages to install:     
    - `google-api-python-client` with these dependencies installed
        - `httplib2`
        - `uritemplate`
         
    
    URLs:
    
    _Repository_     
      https://github.com/googleapis/google-api-python-client      
    _Documentation_      
      https://googleapis.github.io/google-api-python-client 

      
2. **Google Drive**
    
    From the surface, based on current available guides and code samples the library
    for Google Suite... I mean Workspace, is unified. But if you're naive enough to 
    think you can find the library from search engines results, you might land on their 
    old organization page instead https://github.com/googleworkspace/. 
    It still exists, and there's repository for [samples of Python codes](https://github.com/googleworkspace/python-samples), too.     
    If you need a Python library for Google Drive, you'll see they made a client 
    called [`PyDrive`](https://github.com/googleworkspace/PyDrive). 
    Skim the steps in their README, it seems like it's a user friendly library to interact 
    with the Drive API. You'll find that while the module code was last maintained 2 years
    ago, their README is recent, so you jump to the conclusion that it's fine.     
    You'd be mistaken.

    PyDrive's authentication is still using [deprecated oauth2client](https://github.com/googleworkspace/PyDrive/blob/871f7d644dd5df1c6190f7c7eebbab9721ccd4f4/pydrive/auth.py#L4).
    The same can be found in [their `python-samples` repository](https://github.com/googleworkspace/python-samples/commit/d37d8bb05630061f22cc618d75fa831c78412945#diff-a6aff07e06ccae30cfd0c32f52deda0467f1e31ac2d95f2a6de7c231a08b8d1f).     
    If you read carefully, you'll find in PyDrive's `README` file they listed a link to a 
    different repository https://github.com/gsuitedevs/. This other repository name used 
    to be repository for any G Suite libraries, you can't it anymore if you use Github search.
    If you do open that link it will redirect to `googleworkspace` PyDrive repository. 
    This `README` files was last updated just 24 days ago. Dig deeper and you'll find that
    their `development` branch has not been updated for 4 years.   
    
    You should not take their words on what seems obvious when it comes to their codes, 
    although I have to admit that situation in 2020 is _better_ than before. 
    It was just a big clusterfuck and hard to figure out, everything was all over the place.
    
    So what should we use? I have no idea at the moment. Same with **Google Sheets**.
    Most likely I'll use parts of their codes to build my own.

------

##### Google Cloud Client libraries

**Attention**: **_Any description about product limits or pricing in here are severely oversimplified_**.    

> As with any enterprise cloud platforms, everything related to pricing and billing will **_not_** be obvious, in **_short_** list, or **_easy to explain_** without sample case scenario or long descriptions; they are full of gotchas because these are complex infrastructures. **_Any excess usage will be charged_**.     
> 
> **_Read the quotas and pricing pages before usage_**.

Complete list & API endpoint reference:     
  https://cloud.google.com/python/docs/reference       
Starting point for all google cloud API libraries:       
  https://github.com/googleapis/google-cloud-python


1. **BigQuery**     
      BigQuery has free tier quota and rate limit of 10GB active data storage and 1TB of queries processing per month. See https://cloud.google.com/bigquery/quotas for quota and rate limits details, and https://cloud.google.com/bigquery/pricing for breakdowns on pricing and billing     
  
    REST API reference:
    https://cloud.google.com/bigquery/docs/reference/rest
  
    Package to install:
    - `google-cloud-bigquery` - see https://pypi.org/project/google-cloud-bigquery/ for latest version.     
    - (optional for distributed tracing) `google-cloud-bigquery[opentelemetry]`,  `opentelemetry-exporter-google-cloud`. See https://opentelemetry-python.readthedocs.io/ for OpenTelemetry documentation.

    URLs:    
    _Repository_      
    https://github.com/googleapis/python-bigquery        
    _Documentation_       
    https://googleapis.dev/python/bigquery/latest

2. TBD


##### Irrelevant but potentially misleading Google links for Python API developers/users


- https://github.com/google/apis-client-generator - No support for Python here.      
- https://github.com/googleapis/googleapis - Unless you want to be a contributor to one of their repositories, or make a big application using lots of Google APIs, or Java developer, this is most likely irrelevant to you.     
- https://github.com/googleapis/google-auth-library-python-httplib2 - This library is intended to help existing users of `oauth2client` migrate to `google-auth`.
