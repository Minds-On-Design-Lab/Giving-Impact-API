# Campaigns

Campaigns can represent any number of fundraising efforts from walks, to bowl-a-thons, to simple open-ended online giving. Depending on the type of fundraising effort you are running there are various campaign settings you may choose to set up including donation levels, custom data collection fields, and one of the most important, whether the campaign can have Giving Opportunities.  

Giving Opportunities are used to setup teams within a Campaign and as such are perfect to use for events such as walks, bowl-a-thons, or other peer to peer initiatives. They represent unique fundraising opportunities within a parent campaign. Each Giving Opportunity can track donations, shares, and other data uniquely as well as all of these data aggregate up to the parent campaign. This allows you to track the support given to the Campaign as a whole along with that for each individual Giving Opportunity within the Campaign.

## Working With Campaigns

- [The Campaign Object](#the-campaign-object)
- [List Campaigns](#list-campaigns)
- [Retrieve a Campaign](#retrieve-a-campaign)
- [Create a Campaign](#create-a-campaign)
- [Update a Campaign](#update-a-campaign)

## The Campaign Object

The following details each attribute associated with the Campaign object.

### Attributes

name | type | description
------- | ----- | ------------
id_token | string | unique identifier for the Campaign
status | boolean | true/false, used to define if Campaign is active or not
title | string | Campaign name
description | text | description maintains "\n" and "\r\n" and allows the following tags: `<p>, <a>, <strong>, <em>, <b>, <i>, <br>, <ol>, <ul>, <li>`
donation_url | string | fully qualified URL to the hosted donation checkout
| donation_target | decimal | campaign fundraising goal
| donation_minimum | decimal | default is 5.00, minimum donation accepted
| donation_total | decimal | current total
| total_donations | int | current count of donations made
| enable_donation_levels | boolean | true/false, default is false, used to define whether donation levels should be employed or not
has_giving_opportunities | boolean | true/false, defaults to false, used to enable the use of Giving Opportunities within the Campaign
total_opportunities | int | count of Giving Opportunities associated with the Campaign
share_url | string | fully qualified URL to the hosted share page
shares_fb | int | count of instances of Facebook shares made through hosted share functionality
shares_twitter | int | count of instances of Twitter tweets made through hosted share functionality
image_url | string | fully qualified URL to the hosted Campaign image - original file. Userd in hosted checkout.
thumb_url | string | fully qualified URL to the hosted Campaign image - thumbnail file. Used in hosted checkout.
youtube_id | string | YouTube ID for video to display with Campaign. Used in hosted checkout.
hash_tag | string | Twitter hash tag, should include the # e.g., #givingimpact. Used in hosted share.
analytics_id | string | Google analytics profile id associated with the Campaign which when present enables ecommerce tracking on hosted donation checkout and share pages e.g., UA-1234567-12
campaign_color | string | HEX color code used on hosted checkout/share and receipt emails for accent and header background colors
header_font_color | string | HEX color code used for header font on hosted checkout/share and receipt emails.
display_donation_total | boolean | true/false, used to note a preference to show/hide current donation total on hosted checkout
display_donation_target | boolean | true/false, used to note a preference to show/hide donation target on hosted checkout

#### Hash: donation_levels

Includes each donation level

name | type | description
------- | ----- | ------------
level_id | int | unique identifier for level
amount | decimal | value of level
label | string | label/description of level
position | int | used to define the order of levels for display

#### Hash: receipt

Contains all donation email receipt related data

name | type | description
------- | ----- | ------------
send_receipt | boolean | true/false, defaults to false, used to turn on/off automated sending of an email receipt
email_org_name | string | name of organization used in email
reply_to_address | string | email address that should be used as reply to address
bcc_address | string | email address that should be used as BCC address
street_address | string | first line of address
street_address_2 | string | second line of address
city | string  | |
state  | string  | |
postal_code | optional, string | |
country | string  | |
receipt_body  | text | body text of email receipt, maintains "\n" and "\r\n"

#### Hash: custom_fields

Used to define data collection fields for a supporter to complete during the donation checkout process.

name | type | description
------- | ----- | ------------
field_id | int | unique identifier for field
field_type | enum | defines the type of field, accepts either "dropdown" or "text"
field_label | string | label displayed to the donor to describe the field
options | array | used define each option of a dropdown field type, only a value for options is supported
position | int | used for ordering custom_fields through the Dashboard or elsewhere
status | boolean | true/false, defaults to true, used to control preference for whether field is active or inactive
required | boolean |  true/false, defaults to false, used to control field validation

#### Hash: campaign_fields

Used to define data collection fields for Giving Opportunities collected at creation/management.

name | type | description
------- | ----- | ------------
field_id | int | unique identifier for field
field_type | enum | defines the type of field, either "dropdown" or "text"
field_label | string | label displayed to the Giving Opportunity creator to describe the field
options | array | used define each option of a dropdown field type, only a value for options is supported
position | int | used for ordering custom_fields through the Dashboard or elsewhere
status | boolean | true/false, defaults to true, used to control preference for whether field is active or inactive
required | boolean |  true/false, defaults to false, used to control field validation

## List Campaigns

The following methods and arguments are used to return a list of Campaigns.

```json
{
  "error": false,
  "campaigns": [
    {
      "id_token": "123abcdefg",
      "status": true,
      "title": "Walk Campaign",
      "description": "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
      "donation_url": "https://app.givingimpact.com/initiate_donation/123abcdefg",
      "donation_target": "500.00",x
      "donation_minimum": "10.00",
      "donation_total": "200.00",
      "total_donations": "4",
      "enable_donation_levels": false,
      "donation_levels": [],
      "has_giving_opportunities": true,
      "total_opportunities": "3",
      "share_url": "https://app.givingimpact.com/initiate_share/123abcdefg",
      "shares_fb": "5",
      "shares_twitter": "10",
      "image_url": "http://ourcdn.com/campaign_images/112/_original.jpg",
      "thumb_url": "http://ourcdn.com/campaign_images/112/_thumb.jpg",
      "youtube_id": "abCdEf1234",
      "hash_tag": "#walkcampaign",
      "analytics_id": "UA-1234567-11",
      "campaign_color": "#000000",
      "header_font_color": "#ffffff",
      "display_donation_target": true,
      "display_donation_total": true,
      "receipt": {
        "send_receipt": false,
        "email_org_name": "",
        "reply_to_address": "",
        "bcc_address": "",
        "street_address": "",
        "street_address_2": "",
        "city": "",
        "state": "",
        "postal_code": "",
        "country": "",
        "receipt_body": ""
      },
      "custom_fields": [
        {
          "field_id": "47",
          "field_type": "text",
          "field_label": "Donation Message",
          "options": [],
          "position": "1",
          "status": true,
          "required": false
        }
      ]
    },
    {
      "id_token": "456abcdefg",
      "status": true,
      "title": "Holiday Fundraiser",
      "description": "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
      "donation_url": "https://app.givingimpact.com/initiate_donation/456abcdefg",
      "donation_target": "10000.00",
      "donation_minimum": "25.00",
      "donation_total": "3500.00",
      "total_donations": "40",
      "enable_donation_levels": true,
      "donation_levels": [
        {
          "amount": "25.00",
          "label": "Silver",
          "position": "1"
        },
        {
          "amount": "100.00",
          "label": "Gold",
          "position": "2"
        },
        {
          "amount": "500.00",
          "label": "Platinum",
          "position": "3"
        }
      ],
      "has_giving_opportunities": false,
      "total_opportunities": "0",
      "share_url": "https://app.givingimpact.com/initiate_share/456abcdefg",
      "shares_fb": "5",
      "shares_twitter": "10",
      "image_url": "http://ourcdn.com/campaign_images/112/_original.jpg",
      "thumb_url": "http://ourcdn.com/campaign_images/112/_thumb.jpg",
      "youtube_id": "abCdEf1234",
      "hash_tag": "#holidaycampaign",
      "analytics_id": "UA-1234567-12",
      "campaign_color": "#000000",
      "header_font_color": "#ffffff",
      "display_donation_target": true,
      "display_donation_total": true,
      "receipt": {
        "send_receipt": false,
        "email_org_name": "",
        "reply_to_address": "",
        "bcc_address": "",
        "street_address": "",
        "street_address_2": "",
        "city": "",
        "state": "",
        "postal_code": "",
        "country": "",
        "receipt_body": ""
      },
      "custom_fields": [
        {
          "field_id": "48",
          "field_type": "dropdown",
          "field_label": "Is this your first time donating to us?",
          "options": [
            "Yes",
            "No"
          ],
          "position": "1",
          "status": true,
          "required": false
        }
      ]
    }
  ]
}
```

Get a list of all of an account's active campaigns with the following GET request:

	/campaigns

or

	/campaigns?status=active

Get a list of all of an account's inactive campaigns with the following GET request:

	/campaigns?status=inactive

Get a list of all of an account's campaigns including both active and inactive with the following GET request:

	/campaigns?status=both

## Retrieve a Campaign

Get a specific campaign with the following GET request:

	/campaigns/{id_token}


## Create a Campaign

You can create a new Campaign by sending a POST request to the following URI.

    /campaigns

In addition to the authentication and user-agent headers, the following header is also required for POST requests:

    Content-Type: application/json

### Example Post Body

```json
{
  "status": true,
  "title": "The Ultimate Bowl-a-thon!!!",
  "description": "Create your team. Gather your uniforms. Knock some pins. Support us to do more good.",
  "donation_target": "5000.00",
  "donation_minimum": "10.00",
  "enable_donation_levels": false,
  "has_giving_opportunities": true
}
```

[Complete new Campaign example](https://gist.github.com/mindsondesignlab/2f3d76a0696e8ce34da2)


### Required Arguments

The following documents the required arguments.

name | required | type/details
------- | ----- | ------------
status | required | boolean, true/false
title | required | string
description | required | text, description maintains "\n" and "\r\n" and allows the following tags: `<p>, <a>, <strong>, <em>, <b>, <i>, <br>, <ol>, <ul>, <li>`

## Update a Campaign

You can update an existing Campaign by sending a POST request to the following URI where {id_token} is the unique id for the Campaign you would like to update.

     /campaigns/{id_token}

In addition to the authentication and user-agent headers, the following header is also required for POST requests:

     Content-Type: application/json
