---
title: Getting Started
_template: docs
summary: |
  <p>
  	Getting started with our API including resource URLs, Authentication, and versioning.
  </p>
meta_keywords: api, fundraising api, donation api
meta_description: >
  ​Getting started with our API
  including resource URLs, Authentication,
  and versioning.
section: Integration (API)
tags:
  - API
  - resource urls
  - authentication
  - versioning
---
We've designed our API to lead to a **refreshingly simple and customizable** experience. If you are brand new to Giving Impact, we'd recommend giving our [general introduction docs](/docs/introduction/getting-started) a read. For those ready to get to integrating, please, engage!

### API Endpoint

	https://app.givingimpact.com/api/{version}

### Resource URL Patterns

- /campaigns
- /campaigns/{id_token}
- /campaigns/{id_token}/donations
- /campaigns/{id_token}/opportunties
- /opportunities/{id_token}
- /opportunities/{id_token}/donations
- /donations/{id_token}
- /campaigns/{id_token}/stats/log
- /campaigns/{id_token}/stats/range
- /opportunities/{id_token}/stats/log
- /opportunities/{id_token}/stats/range


Authentication
--------------

Authentication requires a valid API Key for the account as well as providing a User-Agent.

* API Key - A string provided by Giving Impact.  Keys are unique to a subscribing account.
* User-Agent - A string describing the site or application using the API.

Both are provided as headers as follows:

### API Key  
     X-GI-Authorization: {api-key-string}

### User-Agent  
     User-Agent: {user-agent-string}

### Content-Type (Required for POST)
	Content-Type: application/json

Versioning
----------

Current Stable Version: **v2**

You specify the version of the API you would like use by adding the version number to the API URL as follows:

	https://app.givingimpact.com/api/v2/...

### Version History

* v2 - **Current** Release