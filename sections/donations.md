# Working With Donations

- [The Donation Object](#the-donation-object)
- [List Donations](#list-donations)
- [Retrieve a Donation](#retrieve-a-donation)
- [The Magic Related Parameter](#the-magic-related-parameter)
- [Create an Offline Donation](#create-an-offline-donation)
- [Update an Existing Donation](#update-an-existing-donation)

## The Donation Object

The following details each attribute uniquely associated with the Donation object.

### Attributes

name | type | description
------- | ----- | ------------
id_token | string | unique identifier for the donation
donation_date | timestamp | YYYY-MM-DD HH:MM::SS, date/time of donation
campaign -or- opportunity | string | unique identifier for the parent campaign or opportunity
first_name | string | donor first name
last_name | string | donor last name
billing_address1 | string | billing address
billing_city | string | billing city
billing_state | string | state
billing_postal_code | string | billing postal code
billing_country | string | billing country
donation_total | int | donation amount
donation_level | string | if a donation level was selected, would include the level label
donation_level_id | int | unique identifier for level selected
contact | boolean | true/false, used to define if donor opted out of being contacted by email
email_address | string | email address of donor
offline | boolean | true/false, used to define if donation was recorded as an "offline" donation or not
twitter_share | boolean | true/false, used to define if donor shared via Twitter at end of donation checkout
facebook_share | boolean | true/false, used to define if donor shared via Facebook at end of donation checkout

#### Hash: custom_responses

Includes donors responses to any custom fields added to donation checkout.

name | type | description
------- | ----- | ------------
field_id | int | unique id for the custom field
field_type | enum | defines the type of field, accepts either "dropdown" or "text"
field_label | string | label displayed to the donor to describe the field
response | string | donors response
status | boolean | true/false, defaults to true, used to control preference for whether field is active or inactive

## List Donations

### Get a list of all of a Campaign's Donations

This includes all donations made to children Giving Opportunities as well as those made to the main campaign directly.

You can retrieve a list by sending a GET request to the URI with the following format:

	/campaigns/{id_token}/donations

#### Response

```json
{
    "error": false,
    "donation": {
        "id_token": "a5f105f445",
        "donation_date": "2013-03-01 10:37:52",
        "campaign": "c5bb65d34b",
        "first_name": "Test",
        "last_name": "Donor",
        "billing_address1": "100 Brooklyn St",
        "billing_city": "Brooklyn",
        "billing_state": "New York",
        "billing_postal_code": "11201",
        "billing_country": "United States",
        "donation_total": "50.00",
        "donation_level": "",
        "donation_level_id": "",
        "contact": true,
        "email_address": "support@givingimpact.com",
        "offline": false,
        "twitter_share": false,
        "fb_share": false,
        "custom_responses": [
            {
                "field_id": "123",
                "field_type": "text",
                "field_label": "Donation Message",
                "response": "I think this is a stellar cause, wish I could join the walk with a team.",
                "status": true
            },
            {
                "field_id": "124",
                "field_type": "dropdown",
                "field_label": "How did you hear about this cause?",
                "response": "Facebook",
                "status": true
            }
        ],
        "supporter": {
            id_token: "2fea64d8ac",
            first_name: "Test",
            last_name: "Donor",
            email_address: "support@givingimpact.com",
            street_address: "100 Brooklyn St",
            city: "Brooklyn",
            state: "NY",
            postal_code: "11201",
            country: "United States",
            donations_total: "100",
            total_donations: "2"
        }
    }
}
```

### Get a list of all of a Giving Opportunty's Donations

Please note, if a donor opts out for email follow-ups, their email address will not be returned.

You can retrieve a list by sending a GET request to the URI with the following format:

	/opportunities/{id_token}/donations


## Retrieve a Donation

You can retrieve a single donation by sending a GET request to the URI with the following format:

	/donations/{id_token}


## The Magic "Related" Parameter

There are times when the Donation object data is not enough and you simply need the parent Campaign or Giving Opportunity's data as well. Sometimes you will just want to know the name of the "team" the donation was made to. Whatever your need or reason, all you need to do is pass the following parameter to either your list or specific Donation calls to get the relate parent Campaign or Giving Opportunity's data as well.

	related: true


## Create an "Offline" Donation

Donations recorded through the checkout are documented as part of that process; however, there are times when an donation outside of this workflow is made and it may be desirable to account for it. We call these donations "offline" and they can be added created/updated through the API or Dashboard and can be used for such things as to note when checks or cash donations are made to name a couple.

You can create a new "offline" donation by sending a POST request to the following URI.

    /donations

In addition to the authentication and user-agent headers, the following header is also required for POST requests:

    Content-Type: application/json

### Example Post Body

```json
{
  "campaign": "1234abcde",
  "donation_date": "2013-05-16 20:00:00",
  "first_name": "Greedo",
  "last_name": "TheElder",
  "billing_address1": "100 Best Spot",
  "billing_city": "Mos Eisley Cantina",
  "billing_state": "Tatooine",
  "billing_postal_code": "10001",
  "billing_country": "United States",
  "donation_total": "50.00",
  "donation_level": "",
  "contact": true,
  "email_address": "greedo@givingimpact.com"
}
```

### Arguments

The following documents the required arguments.

name | required | type/details
------- | ----- | ------------
campaign -or- opportunity | required | string, unique identifier for the parent campaign or opportunity
donation_date | | timestamp, YYYY-MM-DD HH:MM:SS, time of donation
first_name | required | string, donor first name
last_name | required | string, donor last name
billing_address1 | required | string, billing address
billing_city | required | string, billing city
billing_state | required | string, state
billing_postal_code | required | string, billing postal code
billing_country | required | string, billing country
donation_total | required| int, donation amount
donation_level_id | | int, unique identifier for level selected
contact | required | boolean*, true/false, used to define if donor opted out of being contacted by email
email_address | required | string, email address of donor

#### Hash: custom_responses

Includes donors responses to any custom fields added to donation checkout.

name | required | type/details
------- | ----- | ------------
field_id | | int, unique id for the custom field
response | | string, donors response


## Update an Existing Donation

You can update an existing "Offline" or online donation by sending a POST request to the following URI where {id_token} is the unique id for the donation you would like to edit.

     /donations/{id_token}

In addition to the authentication and user-agent headers, the following header is also required for POST requests:

     Content-Type: application/json

### Implementation Details

- To keep things simple you can pass only those data that you would like to update. Any data for elements not posted will stay the same.
- You cannot change a donation from "offline" to "online" or the opposite via an update.
- You cannot associate a donation to another Campaign or Giving Opportunity.
