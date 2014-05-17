# Stats 

Access aggregate data to generate activity logs and reports.

- [The Stats Object](#the-stats-object)
- [Stats Log](#stats-log)
- [Stats Range](#stats-range)

## The Stats Object

The following details each attribute uniquely associated with the Stats object.

### Attributes

name | type | description
------- | ----- | ------------
total_donations | int | total number of donations
shares_fb | int | total number of facebook shares
shares_twitter | int | total number of twitter shares
donation_total | decimal | sum total of donation amount
date | date | YYYY-MM-DD


## The Stats Log

### Get a list of log entries for a Campaign

	/campaigns/{id_token}/stats/log

#### Sample Response

<script src="https://gist.github.com/mindsondesignlab/aaa9a161ce7454cd858d.js"></script>

### Get a list of log entries for a Giving Opportunity

	/opportunities/{id_token}/stats/log

## The Stats Range

The Stats Range method accepts two unique parameters allow you to request log entries using dates.

name | type | description
------- | ----- | ------------
before | timestamp | YYYY-MM-DD
after | timestamp | YYYY-MM-DD

### Get a list of log entries for a Campaign between two dates

	/campaigns/{id_token}/stats/range?after=YYYY-MM-DD&before=YYYY-MM-DD

### Get a list of log entries for a Giving Opportunity between two dates

	/opportunties/{id_token}/stats/range?after=YYYY-MM-DD&before=YYYY-MM-DD
