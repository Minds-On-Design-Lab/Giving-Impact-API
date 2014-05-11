All API methods support parameters to *sort*, *limit*, and *offset* results. These are useful tools to allow you to address any number of scenarios including but not limited to the following.

* Pagination using *offset* and *limit*
* Show top three teams using *limit* and *sort*
* Show ten most recent donors using *limit* and *sort*

These parameters are appended to the query string in traditional GET request format:

	<REQUEST>?limit=<INT>&offset=<INT>&order=<PROPERTY>[|<DIRECTION>] 

If offset is omitted, **0** is assumed. Direction is optional and defaults to **ASC** (ascending).

### Examples ###

Return 10 Campaigns:
	
	/campaigns?limit=10 

Return 8 Campaigns, skipping the first 20:

	/campaigns?limit8&offset=20

Return 10 Campaigns, ordered by donation_total:

	/campaigns?limit=10&sort=donation_total 

Return 10 Campaigns, ordered by most funded first:

	/campaigns?limit=10&sort=donation_total|desc

*Note the pipe ("|") character between donation_total and desc. The sort value can be any valid attribute.*

Return 3 Giving Opportunties, ordered by the most donations received:

	/campaigns/{id_token}/opportunities?limit=3&sort=total_donations|desc
	
Return 10 most recent Campaign donors:

	/campaigns/{id_token}/donations?limit=10&sort=donation_date|desc