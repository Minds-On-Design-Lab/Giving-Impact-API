# Giving Impact - Stripe Online Fundraising

Giving Impact™ is designed to build on Stripe to provide you with the tools to create powerful online fundraising solutions.

Our suite of tools includes a fantastic dashboard for managing your fundraising initiatives and an API that allows your web development partners to create rich landing pages more efficiently.

We've designed our API to lead to a **refreshingly simple and customizable** experience. If you are brand new to Giving Impact, we'd recommend giving our [general introduction docs](http://givingimpact.com/docs/introduction/getting-started) a read. For those ready to get to integrating, please, engage!

## API Endpoint

	https://app.givingimpact.com/api/{version}

## Resource URL Patterns

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

## Authentication

Authentication requires a valid API Key for the account as well as providing a User-Agent.

* API Key - A string provided by Giving Impact.  Keys are unique to a subscribing account.
* User-Agent - A string describing your site or application that is using the API.

Both are provided as headers as follows:

### API Key  
     X-GI-Authorization: {api-key-string}

### User-Agent  
     User-Agent: {user-agent-string}

### Content-Type (Required for POST)
	Content-Type: application/json

## Versioning

Current Stable Version: **v2**

You specify the version of the API you would like use by adding the version number to the API URL as follows:

	https://app.givingimpact.com/api/v2/...

### Version History

* v2 - **Current** Release

## API Available

- [Campaigns](sections/campaigns.md)
- [Giving Opportunities](sections/opportunities.md)
- [Donations](sections/donations.md)
- [Stats](sections/stats.md)

## Additional Docs

- [Donation Checkout](sections/donation-checkout.md)
- [Webhooks](sections/webhooks.md)
- [API Errors](sections/errors.md)
- [Sorts, Limits, and Offsets](sections/using-sorts-limits-offsets.md)

## API Libraries

- [GivingImpact PHP](https://github.com/Minds-On-Design-Lab/givingimpact-php) - PHP Library