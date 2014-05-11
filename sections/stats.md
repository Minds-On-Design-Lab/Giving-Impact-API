---
title: Reports (Stats)
_template: docs
summary: |
  <p>
  	The Stats object and log and range methods that are useful for creating campaign progress reports.
  </p>
meta_keywords: >
  reports, stats, metrics, reports api,
  donation reports api, fundraising api,
  fundraising reports
meta_description: >
  The Stats object and log and range
  methods that are useful for creating
  campaign progress reports.
section: Integration (API)
tags:
  - stats
  - metrics
  - progress
  - reports
---
- [The Stats Object](#object)
- [Stats Log](#log)
- [Stats Range](#list)

<a id="object"></a>

The Stats Object
-----------------------------

The following details each attribute uniquely associated with the Stats object.

### Attributes

total_donations
: *int*, total number of donations

shares_fb
: *int*, total number of facebook shares

shares_twitter
: *int*, total number of twitter shares

donation_total
: *decimal*, sum total of donation amount

date
: *date*, YYYY-MM-DD

<a id="log"></a>

The Stats Log
-----------------------------

### Get a list of log entries for a Campaign

	/campaigns/{id_token}/stats/log

#### Sample Response

<script src="https://gist.github.com/mindsondesignlab/aaa9a161ce7454cd858d.js"></script>


### Get a list of log entries for a Giving Opportunity

	/opportunities/{id_token}/stats/log

<a id="Range"></a>

The Stats Range
-----------------------------

The Stats Range method accepts two unique parameters allow you to request log entries using dates.

before
: *timestamp*, YYYY-MM-DD

after
: *timestamp*, YYYY-MM-DD

### Get a list of log entries for a Campaign between two dates

	/campaigns/{id_token}/stats/range?after=YYYY-MM-DD&before=YYYY-MM-DD

### Get a list of log entries for a Giving Opportunity between two dates

	/opportunties/{id_token}/stats/range?after=YYYY-MM-DD&before=YYYY-MM-DD
