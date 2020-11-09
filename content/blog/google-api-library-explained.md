---
title: "Google's official API client libraries explained"
date: 2020-11-09T16:23:40Z
tags: [ 'development','python' ]
draft: false
---

The goal of this short explanation is to attempt to maintain a placeholder for
self reminder, creating a central bookmark on important (relevant) links that
reflect their most current state on library for services, as they have somewhat
complex to navigate sites for official libraries. Not as unusable as Microsoft or several other dinosaur companies, but enough to waste non trivial amount of time.      In the past I've encountered
period of limbo, around 2017 to early 2019, where few of their client library
were stuck in a state of deprecation without clear direction on what that means for users.         
This sounds like it was not a big deal except I found this out when I needed OAuth library,
which cost me days of sorting out confusing, conflicting informations given
in their developer guides and the library package documentation site.

They're also infamous for killing products _and_ changing brands, and it seems to me
they only started to make an effort for streamlined, unified libraries & documentations
in recent few years (at least for Python libraries), as there are still some old
tutorials & guides on their pages that are not updated yet, which can mislead users.

Figuring out their ins & out haven't been fun, I found re-learning is even less fun.      
So I'm brain dumping it here since I immensely dislike having to browse & read
massive enterprise pages full of vague lingos just to figure out vague Java method procedures that they're using as backend.

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
but for basic users a.k.a non paying clients, seems like there's no way 
to have a central, codeless admin dashboard to orchestrate or administrate, 
so these type of users have to go through individual documentation
for each library.

Complete list to their products for developers can be found in
  https://developers.google.com/products/develop

&nbsp;&nbsp;&nbsp;&nbsp;

Below are the relevant Python libraries.

##### Google Auth Python library

I'm not a fan of sending out API keys embedded in url requests like from `curl` or any other
methods, so OAuth is essential for avoiding that, as well as future proofing identification 
procedure for any API activities inside any apps.

It turns out that there's somewhat ambiguous URI for developer console related with authentication API at https://console.developers.google.com/, I'm sure this detail has escaped me entirely before.     
It's the same dashboard for cloud services administration, only with limited features and different title (`Google APIs` instead of `Google Cloud Platform`).

![Google APIs dashboard](/static/img/googleapis_dashboard.png) ![Google Cloud Platform dashboard](/static/img/googlecloudplatform_dashboard.png) 

 AFAIK there's no attempt to explain the real difference between the two, other than the obvious conclusion that one discerns after the fact of learning that there are two dashboards, and the titled Cloud Platform is for enterprise customers. It's probably clear and normal to some people but I find it not very user friendly to have different entry points without any clear patterns or context, it's a little disorienting.

Packages:    
  
- `google-auth` see https://pypi.org/project/google-auth for latest version.      
- `google-auth-oauthlib` see https://pypi.org/project/google-auth-oauthlib for latest version.

URLs:

_Repository_       
  https://github.com/googleapis/google-auth-library-python      
_Documentation_       
  https://googleapis.dev/python/google-auth/latest  

Note:      
  Support async
  

##### Google Suite client libraries

1. **Google API Python library**

    Honestly I have no fucking idea what exactly this is for/why it exists, I'm guessing it's either to be used in conjuction with the real libraries or to serve people who likes directly interacting with API endpoints. The docs homepage only offered this explanation     

    > The Google API Client Library for Python is designed for Python client-application developers. It offers simple, flexible access to many Google APIs.

    with these TOC guides     

    > * Getting started 
    > * Auth ...
    > * How to…    
    >   * Use Logging     
    >   * Upload Media    
    >   * Use Mocks    
    > ...etc
    
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
3. **Google Sheets**



##### Google Cloud Client libraries


Complete list & API endpoint reference:     
  https://cloud.google.com/python/docs/reference       
Starting point for all google cloud API libraries:       
  https://github.com/googleapis/google-cloud-python


1. **BigQuery**     
  BigQuery has free tier quota and rate limit of 10GB active data storage and 1TB of queries processing per month, but as with any enterprise cloud services these are not the complete descriptions, any excess usage will be charged. See https://cloud.google.com/bigquery/quotas for quota and rate limits details, and https://cloud.google.com/bigquery/pricing for breakdowns on pricing and billing     
  
  REST API reference:
   https://cloud.google.com/bigquery/docs/reference/rest
  
  Package to install:
  - `google-cloud-bigquery` see https://pypi.org/project/google-cloud-bigquery/ for latest version.     
  - (optional for distributed tracing) `google-cloud-bigquery[opentelemetry]`,  `opentelemetry-exporter-google-cloud`. See https://opentelemetry-python.readthedocs.io/ for OpenTelemetry documentation.

  URLs:    
  _Repository_      
  https://github.com/googleapis/python-bigquery        
  _Documentation_       
  https://googleapis.dev/python/bigquery/latest

