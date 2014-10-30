# Working With Supporters

- [The Supporter Object](#the-supporter-object)
- [List Supporters](#list-supporters)
- [Retrieve a Supporter](#retrieve-a-supporter)
- [Create a Supporter](#create-a-supporter)
- [Update an Existing Supporter](#update-an-existing-supporter)

## The Supporter Object

The following details each attribute uniquely associated with the Supporter object.

### Attributes

name | type | description
------- | ----- | ------------
id_token | string | unique identifier for the supporter
first_name | string | first name
last_name | string | last name
street_address | string | street address
city | string | city
state | string | state
postal_code | string | postal code
country | string | country
donations_total | int | total donation amount by supporter

## List Supporters

### Get a list of all of your account's supporters

This includes all supporters across all campaigns

You can retrieve a list by sending a GET request to the URI with the following format:

  /supporters/

#### Response

```json
{
  error: false,
  supporters: [
    {
      id_token: "2fea64d8ac",
      first_name: "Test",
      last_name: "Donor",
      email_address: "testdonor@something.com",
      street_address: "159 Somewhere St.",
      city: "Brooklyn",
      state: "NY",
      postal_code: "11201",
      country: "United States",
      donations_total: "20",
      total_donations: "1"
    },
    {
      id_token: "fdc9741077",
      first_name: "Jill",
      last_name: "Friend",
      email_address: "someone@bklyn.com",
      street_address: "1 Atlantic Ave",
      city: "Brooklyn",
      state: "NY",
      postal_code: "11201",
      country: "US",
      donations_total: "150",
      total_donations: "2"
    }
  ]
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

<script src="https://gist.github.com/mindsondesignlab/6938fb105e539c6e14ca.js"></script>

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
