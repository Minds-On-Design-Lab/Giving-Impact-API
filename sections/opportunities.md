# Working With Giving Opportunities

- [The Giving Opportunity Object](#the-giving-opportunity-object)
- [List Giving Opportunities](#list-giving-opportunities)
- [Retrieve a Giving Opportunity](#retrieve-a-giving-opportunity)
- [Opportunities by Supporter](#opportunities-by-supporter)
- [The Magic "Related" Parameter](#the-magic-related-parameter)
- [Create a Giving Opportunity](#create-a-giving-opportunity)
- [Update a Giving Opportunity](#update-a-giving-opportunity)

Giving Opportunities are the buckets within the bucket of a Campaign. Want to setup a team-based Campaign or allow supporters to create their own peer-to-peer fundraising pages for their birthday's? You can use Giving Opportunities to track and manage the activies of these smaller yet crucial efforts and have their results aggregate up to a parent Campaign.

Because a Giving Opportunity has a parent Campaign, it is by design that many features and preferences of the campaign should trickle down to the Giving Opportunity including use of donation levels, custom fields, minimum donation amount, and such. To help access these data we include a [related parameter](#the-magic-related-parameter) that lets you retrieve the full set of campaign data along with that of the opportunity.


## The Giving Opportunity Object

The following details each attribute uniquely associated with the Giving Opportunity object.

### Attributes

name | type | description
------- | ----- | ------------
id_token | string | unique identifier for the Giving Opportunity
status | boolean | true/false, used to define if Giving Opportunity is active or not
title | string | Giving Opportunity name
description | text | description maintains "\n" and "\r\n" and allows the following tags: `<p>, <a>, <strong>, <em>, <b>, <i>, <br>, <ol>, <ul>, <li>`
donation_url | string | fully qualified URL to the hosted donation checkout
donation_target | decimal | Giving Opportunity fundraising goal
donation_total | decimal | current total
total_donations | int | current count of donations made
share_url | string | fully qualified URL to the hosted share page
shares_fb | int | count of instances of Facebook shares made through hosted share functionality
shares_twitter | int | count of instances of Twitter tweets made through hosted share functionality
image_url | string | fully qualified URL to the hosted Giving Opportunity image - original file
thumb_url | string | fully qualified URL to the hosted Giving Opportunity image - thumbnail file
youtube_id | string | YouTube ID for video to display with Giving Opportunity

#### Hash: campaign_responses

Data captured through Campaign Fields setup through the Campaign.

name | type | description
------- | ----- | ------------
campaign_field_id | int | unique identifier for field
field_type | enum | defines the type of field, either "dropdown" or "text"
field_label | string | label displayed to the Giving Opportunity creator to describe the field
response | string | user entered or selected response
status | boolean | true/false, defaults to true, used to control preference for whether field is active or inactive

#### Hash: supporters

Opportunity supporters

name | type | description
------- | ----- | ------------
id_token | string | unique identifier for the supporter
first_name | string | first name
last_name | string | last name
email_address | string | email address
street_address | string | street address
city | string | city
state | string | state
postal_code | string | postal code
country | string | country
donations_total | int | total donation amount by supporter

## List Giving Opportunities

Get a list of all of a Campaign's Giving Opportunties with the following GET request:

	/campaigns/{id_token}/opportunities

### Example Response

```json
{
	"error": false,
	"opportunity": {
		"id_token": "0a13b0fbdb",
		"status": true,
		"title": "Team MOD-Lab",
		"description": "We are team dedicated to this Sample Org and their cause. Here is why we think you should support us and them. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
		"donation_url": "http://app.givingimpact.com/initiate_donation/0a13b0fbdb",
		"donation_target": "300.00",
		"donation_total": "195.00",
		"total_donations": "2",
		"share_url": "http://app.givingimpact.com/initiate_share/0a13b0fbdb",
		"shares_fb": "0",
		"shares_twitter": "1",
		"image_url": "",
		"thumb_url": "",
		"youtube_id": "",
		"campaign_responses": [
			{
				"campaign_field_id": "1",
				"field_type": "text",
				"field_label": "What is your Name?",
				"response": "Thor",
				"status": true
			},
			{
				"campaign_field_id": "2",
				"field_type": "How did you hear about this campaign?",
				"field_label": "A dropdown",
				"response": "Email",
				"status": true
			}
		],
		"supporters": [
			{
				  "id_token": "2fea64d8ac",
				  "first_name": "Test",
				  "last_name": "Donor",
				  "email_address": "testdonor@something.com",
				  "street_address": "159 Somewhere St.",
				  "city": "Brooklyn",
				  "state": "NY",
				  "postal_code": "11201",
				  "country": "United States",
				  "donations_total": "20",
				  "total_donations": "1"
			},
			{
				  "id_token": "fdc9741077",
				  "first_name": "Jill",
				  "last_name": "Friend",
				  "email_address": "someone@bklyn.com",
				  "street_address": "1 Atlantic Ave",
				  "city": "Brooklyn",
				  "state": "NY",
				  "postal_code": "11201",
				  "country": "US",
				  "donations_total": "150",
				  "total_donations": "2"
			}
		]
	}
}
```

## Retrieve a specific Giving Opportunity

You can retrieve a single result by sending a GET request to the URI with the following format:

	/opportunities/{id_token}

## Opportunities by Supporter

You can retrieve a list of opportunities for a supporter by passing the `supporter` parameter:

	/opportunities?supporter=name@example.com

## The Magic "Related" Parameter

There are times when the Giving Opportunity object data is not enough and you simply need the parent Campaign's data as well. Let's say you want the hastag to add to a Tweet button or you simply want the Campaign id_token and title so you can create a breadcrumb link back to the Campaign page. Whatever your need or reason, all you need to do is pass the following parameter to either your list or specific Giving Opportunity calls to get the relate parent Campaign data as well.

	related: true

## Create a Giving Opportunity

You can create a new Giving Opportunity by sending a POST request to the following URI.

		/opportunities

In addition to the authentication and user-agent headers, the following header is also required for POST requests:

		Content-Type: application/json

### Example Post Body

```json
{
	"campaign_token":"{id_token}",
	"title":"String name goes here",
	"description":"Full description goes here. This can be a short paragraph.",
	"donation_target":"500.00",
	"status":true
}
```

### Arguments

The following documents the various arguments accepted.

name | required | type/details
------- | ----- | ------------
campaign_token | required | string, unique id_token for the parent Campaign
status | required | boolean, true/false
title | required | string
description | required | text, description maintains "\n" and "\r\n" and allows the following tags: `<p>, <a>, <strong>, <em>, <b>, <i>, <br>, <ol>, <ul>, <li>`
donation_target | | decimal
image_file | | base64 blob
image_type | | enum, currently accepts “jpg”, “gif”, or “png”, default is “jpg” if image exists, describes the type image_file being sent
youtube_id | | string, can accept just the id or YouTube short URL from which we will extract the id e.g.,  http://youtu.be/C_S5cXbXe–4

#### Hash: custom_response

Used to create or update data collection fields for Giving Opportunity setup as part of Campaign settings.

name | required | type/details
------- | ----- | ------------
campaign_field_id | | int, unique id of field
response | | string, data storing for field response

## Update a Giving Opportunity

You can update an existing Giving Opportunity by sending a POST request to the following URI where {id_token} is the unique id for the Giving Opportunity you would like to edit.

		 /opportunities/{id_token}

In addition to the authentication and user-agent headers, the following header is also required for POST requests:

		 Content-Type: application/json
