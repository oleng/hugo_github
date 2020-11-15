---
title: "Google's official API client libraries explained"      
date: 2020-11-09T16:23:40Z     
tags: [ 'development','python' ]       
draft: false    
---

The purpose of this short explanation is an attempt for a brain dump, to maintain 
a central compilation of relevant links that reflects most current state of Google's 
Python client libraries for their services, as they have somewhat complex to navigate 
sites for official libraries. Not as unusable as Microsoft or several other 
dinosaur companies, but enough to waste non trivial amount of time.

Figuring out their ins & out haven't been fun, I found re-learning is even less fun. 
I immensely dislike having to browse and read pages full of vague lingos just to 
figure out vague Java method procedures that they're using as backend. Thus this post.
Even the process of writing this makes me feel like pulling every single strand of my hair out,
I _really_ hate Java developers mindset on approaching system design, they're borderline cult-ish
in maintaining stance against user friendliness, a.k.a they think everyone should follow their ways
because only Java developers know what's best.    

![driven crazy by Google's ways](https://i.kinja-img.com/gawker-media/image/upload/s--PVXB4pW3--/cjwxtzqipnoyja39xuoy.jpg)

This also serves as a rant post, at times with profanities, since I think they 
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

_Note 2020/11/11_: Apparently, they do realize they have a problem in providing clear path and
support for developers to use their client libraries. I found that they created a page 
to explain their situation at https://cloud.google.com/apis/docs/client-libraries-explained.   
In there, they claim that Google Cloud client libraries are the recommended, idiomatic
clients for accessing their (Cloud) APIs, which may or may not means that non-Cloud 
products users are basically somewhat fucked because they won't pay as much attention to
those products client libraries. 

_2020/11/15_: Actually, I think non Cloud customers _are_ fucked. They pushed authentication
and authorization libraries that are not just heavily but almost entirely assume Cloud products
developers as primary users, as reflected by their docs both in web and in codes, yet 
there is still no clear clarification on which works for both, which only works for Cloud products, 
and what their recommendations are for non Cloud products without spending hours/days 
hunting them inside each product pages.     

Case in point is documentations for actual permissions for different type of accounts assigned 
by OAuth 2.0 private keys. I received this exception when using `Web server application` account type 
in `google-auth`, intending to access Google Drive API:

    
    import google.auth
    from googleapiclient.discovery import build
    
    # https://developers.google.com/drive/api/v3/about-auth#OAuth2Scope
    DRIVE_SCOPES = [...]
    https://developers.google.com/sheets/api/guides/authorizing#OAuth2Scope
    SHEET_SCOPES = [...]
    
    # file path saved in environment var `GOOGLE_APPLICATION_CREDENTIALS`
    creds = google.auth.default(scopes=DRIVE_SCOPES+SHEET_SCOPES)
    
    # EOF. that's it, that's the entire content of the file.


DefaultCredentialsError: The file "client_secret_<project-id>.apps.googleusercontent.com.json"
    does not have a valid type. Type is None, expected one of ('authorized_user', 'service_account').


Granted that their [quickstart sample](https://developers.google.com/drive/api/v3/quickstart/python#step_3_set_up_the_sample) uses [Authorization Code flow](https://oauth.net/2/grant-types/authorization-code/), as `google-auth` is their official supported library, I expected there'd be compatibility _and_ proper documentation for using it to authenticate and authorize access to Google Drive. 
A universal way to use their OAuth service, and a friendlier guide are not outside of their reach.     
I intent to have this app permission to use BigQuery in the later stage, so with the assumption 
that Cloud's account types should be able to act as an app that interacts with non Cloud product users,
e.g. they have higher accessability to wider range of Google product line up, I created a 
service account. But guess what, turned out I have to give permissions for that service account to 
access my Google Drive. 


    # I created a client object using google.auth.default and got valid credential object
    # from the new service account private key.
    
    >>> client.session
    <google.auth.transport.requests.AuthorizedSession at 0x113f086a0>
    
    >>> client.session._refresh_status_codes[0]
    <HTTPStatus.UNAUTHORIZED: 401>
    
    >>> client.session._refresh_status_codes[0].__dict__
    {'_value_': 401,
     'phrase': 'Unauthorized',
     'description': 'No permission -- see authorization schemes',
     '_name_': 'UNAUTHORIZED',
     '__objclass__': <enum 'HTTPStatus'>}
     
    # What authorization schemes? Where?? 
    # Does it kill you to include documentation page URL?
    

Is this documented? Is there a guide to programatically ask the Google Drive account and files owner
to give a service account their permission? Of course not, I have to spend my limited time on this 
plane of the living to search the internet to figure those out. Minutes by minutes, hour by hour, 
Google costs people all over the world their most precious resource with their incompetence.     
I see more [in-depth pages for Service accounts](https://cloud.google.com/iam/docs/understanding-service-accounts) than any other available options, since service accounts are basically created 
for enterprise customers. However so many limitations and inconveniences introduced by their own system are not easy to find. All of this time wasting confusions caused by lack of clarity is abysimal 
experience for Google standard. Before anyone defends Google with the usual lazy argument that 
Google is a business entity therefore it isn't reasonable to expect more from them, here are 
the reasons we should expect better:     

- People try their products for all kinds of reasons, and very few of them works at multi-national companies with tens of thousands employees/Netflix scale, so less than 100/1000 employees companies
have very different requirements
- Developers promote the tools and services that they personally like to their workplace. It's in Google's self interest to not give developers bad support.      
- Google is one of the giants on earth that affects many people's lives, cost of their mistakes 
is nowhere comparable to normal sized companies, the difference is in magnitudes.
- It's been a common public knowledge that AWS has better documentations.

That kind of argument, or the "if you don't like it don't use it" kind we frequently found on the internet, is absolute logic trash.

&nbsp;&nbsp;&nbsp;&nbsp;

## Overview

At the risk of oversimplifying their product line (I'm totally fine with that),
basically they have two suites for two levels of users/client, Google Cloud and G Suite 
(rebranded as Google Workspace now).

Google Cloud is a product suite for their Cloud services, few has free tier
offering, but most are geared for enterprise billing customers.        
Their product page is https://cloud.google.com/, and their web based management UI is
located at https://console.cloud.google.com/

On lower tier they have Google Workspace, it's also a paid product suite targeted for 
small-medium offices, but most are available for free with better limits than Cloud ones.         
The official page is at https://workspace.google.com, with web based UI management in
  https://admin.google.com

Most of the individual product in G Suite supports API access through their client library, 
but for basic users a.k.a non paying clients, seems like there's no way to have 
a central, codeless admin dashboard to orchestrate or administrate, so these type of 
users have to go through individual documentation for each library.

Complete list to their products for developers can be found in
  https://developers.google.com/products/develop
  
Manage projects in the API Console (more accurately in both Google APIs or 
Google Cloud Platform consoles/dashboard, they serve the same API management features 
such as creating credentials, enabling API access, integration with external domain):     
  https://support.google.com/googleapi#topic=7013279     
  https://support.google.com/googleapi/answer/7015000?hl=en&ref_topic=7014522     


&nbsp;&nbsp;&nbsp;&nbsp;

## Python libraries


------


##### Google Auth Python library

I'm not a fan of sending out API keys embedded in url requests like from `curl` or any other
methods, so OAuth is essential for avoiding that, as well as future proofing identification 
procedure for any API activities inside any apps.

It turns out that there's somewhat ambiguous URI for developer console related with authentication API at [https://console.developers.google.com/](https://console.developers.google.com/), I'm sure this detail has escaped me entirely before.     
It's the same dashboard for cloud services administration, only with limited features and different title (_Google APIs_ instead of _Google Cloud Platform_). They are also linked, Google APIs console is just a subset of Google Cloud console, whichever project you have is reflected on both consoles.

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
  https://googleapis.dev/python/google-auth/latest/user-guide.html

Note:      
  Support async
  
  
------


##### Google Suite client libraries

1. **Google API Python library**

    Honestly I had no fucking idea what exactly this is for/why it exists, 
    I was guessing it's either to be used in conjuction with the real libraries or to force
    people to directly interacting with API endpoints. 
    
    The docs homepage only offered this explanation     

    > _The Google API Client Library for Python is designed for Python client-application developers. It offers simple, flexible access to many Google APIs_.

    with these TOC guides     

    > * Getting started 
    > * Auth ...
    > * How to…    
    >   * Use Logging     
    >   * Upload Media    
    >   * Use Mocks    
    > ...etc
    
    Okaay... But if you go to Google APIs organization page in Github and search for
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
    
    So what should we use? I have no idea at the moment. Same with _Google Sheets_ (although [`gspread`](https://github.com/burnash/gspread) looks nice & actively maintained).
    Most likely I'll use parts of their codes to build my own.     
    Btw, check [this](https://developers.google.com/resources/api-libraries/documentation/sheets/v4/python/latest/index.html) out, 
    it's **Google Sheets API PyDoc documentation** from https://developers.google.com/sheets/api/quickstart/python#further_reading 🤦🏻‍♂️


&nbsp;&nbsp;&nbsp;&nbsp;

##### Google Cloud Client libraries

**Attention**: **_Any description about product limits or pricing in here are severely oversimplified_**.    

> As with any enterprise cloud platforms, everything related to pricing and billing will **_not_** be obvious, in **_short_** list, or **_easy to explain_** without sample case scenario or long descriptions; they are full of gotchas because these are complex infrastructures. **_Any excess usage will be charged_**.     
> 
> **_Read the quotas and pricing pages before usage_**.

Complete list & API endpoint reference:     
  https://cloud.google.com/python/docs/reference       
Starting point for all google cloud API libraries:       
  https://github.com/googleapis/google-cloud-python

This seems worthy to check: https://github.com/sathishvj/awesome-gcp-certifications


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

2. **BigQuery Storage**     
    BigQuery Storage API is enabled in all projects in which the BigQuery API is enabled. 
    But permission needs to be granted for the project and BigQuery table.   
    
    This library is API library to read BigQuery table using rpc-based protocol instead of REST API,
    it will send structured data in a binary serialization format. The current supported format
    are Apache Avro (recommended) and Arrow. 
    This API is not for managing BigQuery resources such as datasets, jobs, or tables, only for 
    table queries. It manages a streaming read session for query to a single table that can
    be split in multiple streams or filtered on subset of columns.
    
    Storage API reference:    
    https://cloud.google.com/bigquery/docs/reference/storage

    Package to install:    
    - `google-cloud-bigquery-storage` 

    URLs:    
    _Repository_     
    https://github.com/googleapis/python-bigquery-storage      
    _Documentation_     
    https://googleapis.dev/python/bigquerystorage/latest     


&nbsp;&nbsp;&nbsp;&nbsp;

------


## Irrelevant but potentially misleading links


- https://github.com/google/apis-client-generator - No support for Python here.      
- https://github.com/googleapis/googleapis - Unless you want to be a contributor to one of their repositories, or make a big application using lots of Google APIs, or Java developer, this is most likely irrelevant to you.     
- https://github.com/googleapis/google-auth-library-python-httplib2 - This library is intended to help existing users of `oauth2client` migrate to `google-auth`.
