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

They're also infamous for killing services or changing brands, and it seems to me
they only started to make an effort for streamlined, unified libraries & documentations
in recent few years (at least for Python libraries), as there are still some old
tutorials & guides that are not updated yet, which can mislead users.

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

Most support API access their client library, but for basic users a.k.a non
paying clients, seems like there's no way to have a central codeless admin dashboard
to orchestrate or administrate, so they have to go through individual documentation
for each library.

Complete list to their products for developers can be found in
  https://developers.google.com/products/develop

&nbsp;&nbsp;&nbsp;&nbsp;

Below are the relevant Python libraries.

##### Google Auth Python library

I'm not a fan of sending out API keys embedded in url requests like from `curl` or any other
methods, so OAuth is essential for avoiding that, as well as future proofing identification 
procedure for any API activities inside any apps.

URLs:

_Repository_       
  https://github.com/googleapis/google-auth-library-python      
_Documentation_       
  https://googleapis.dev/python/google-auth/latest  

Note:      
  Support async
  

##### Google API Python library for Google Suite

URLs:

_Repository_     
  https://github.com/googleapis/google-api-python-client      
_Documentation_      
  https://googleapis.github.io/google-api-python-client 



##### Google Cloud Client libraries


See this page for complete list & API reference:     
  https://cloud.google.com/python/docs/reference       
Starting point for all google cloud API libraries:       
  https://github.com/googleapis/google-cloud-python


URLs:

- BigQuery Python library

  _Repository_      
  https://github.com/googleapis/python-bigquery        
  _Documentation_       
  https://googleapis.dev/python/bigquery/latest

