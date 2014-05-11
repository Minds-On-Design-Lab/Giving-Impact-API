- [The Giving Opportunity Object](#object)
- [List Giving Opportunities](#list)
- [Retrieve a Giving Opportunity](#retrieve)
- [Related Parameter](#related)
- [Create a Giving Opportunity](#create)
- [Update a Giving Opportunity](#update)

Giving Opportunities are the buckets within the bucket of a Campaign. Want to setup a team-based Campaign or allow supporters to create their own peer-to-peer fundraising pages for their birthday's? You can use Giving Opportunities to track and manage the activies of these smaller yet crucial efforts and have their results aggregate up to a parent Campaign.

Because a Giving Opportunity has a parent Campaign, it is by design that many features and preferences of the campaign should trickle down to the Giving Opportunity including use of donation levels, custom fields, minimum donation amount, and such. To help access these data we include a [related parameter](#related) that lets you retrieve the full set of campaign data along with that of the opportunity.

<a id="object"></a>

The Giving Opportunity Object
-----------------------------

The following details each attribute uniquely associated with the Giving Opportunity object.

### Attributes

id_token
: *string*, unique identifier for the Giving Opportunity

status
: *boolean*, true/false, used to define if Giving Opportunity is active or not

title
: *string*, Giving Opportunity name

description
: *text*, description maintains "\n" and "\r\n" and allows the following tags: `<p>, <a>, <strong>, <em>, <b>, <i>, <br>, <ol>, <ul>, <li>`

donation_url
: *string*, fully qualified URL to the hosted donation checkout

donation_target
: *decimal*, Giving Opportunity fundraising goal

donation_total
: *decimal*, current total

total_donations
: *int*, current count of donations made

share_url
: *string*, fully qualified URL to the hosted share page

shares_fb
: *int*, count of instances of Facebook shares made through hosted share functionality

shares_twitter
: *int*, count of instances of Twitter tweets made through hosted share functionality

image_url
: *string*, fully qualified URL to the hosted Giving Opportunity image - original file

thumb_url
: *string*, fully qualified URL to the hosted Giving Opportunity image - thumbnail file

youtube_id
: *string*, YouTube ID for video to display with Giving Opportunity

campaign_responses
: hash, data captured through Campaign Fields setup through the Campaign

<div class="api-hash" markdown="1">
campaign_field_id
: *int*, unique identifier for field

field_type
: *enum*, defines the type of field, either "dropdown" or "text"

field_label
: *string*, label displayed to the Giving Opportunity creator to describe the field

response
: *string*, user entered or selected response

status
: *boolean*, true/false, defaults to true, used to control preference for whether field is active or inactive
</div>


<a id="list"></a>

List Giving Opportunities
-------------------------

Get a list of all of a Campaign's Giving Opportunties with the following GET request:

	/campaigns/{id_token}/opportunities
	
### Example Response

<script src="https://gist.github.com/mindsondesignlab/ab4449cf29b3d98f75bc.js"></script>

<a id="retrieve"></a>

Retrieve a specific Giving Opportunity
-----------------------------------------

You can retrieve a single result by sending a GET request to the URI with the following format:

	/opportunities/{id_token}

<a id="related"></a>

The Magic "Related" Parameter
-----------------------------------

There are times when the Giving Opportunity object data is not enough and you simply need the parent Campaign's data as well. Let's say you want the hastag to add to a Tweet button or you simply want the Campaign id_token and title so you can create a breadcrumb link back to the Campaign page. Whatever your need or reason, all you need to do is pass the following parameter to either your list or specific Giving Opportunity calls to get the relate parent Campaign data as well.

	related: true

<a id="create"></a>

Create a Giving Opportunity
-----------------------------------

You can create a new Giving Opportunity by sending a POST request to the following URI.

    /opportunities

In addition to the authentication and user-agent headers, the following header is also required for POST requests:

    Content-Type: application/json

### Example Post Body

<script src="https://gist.github.com/mindsondesignlab/75b0e9992816ad1a8355.js"></script>

### Arguments

The following documents the various arguments accepted.

campaign_token
: **required**, *string*, unique id_token for the parent Campaign

status
: **required**, *boolean*, true/false

title
: **required**, *string*

description
: **required**, *text*, description maintains "\n" and "\r\n" and allows the following tags: `<p>, <a>, <strong>, <em>, <b>, <i>, <br>, <ol>, <ul>, <li>`

donation_target
: optional, *decimal*

image_file
: optional, *base64 blob*

image_type
: optional, *enum*, currently accepts “jpg”, “gif”, or “png”, default is “jpg” if image exists, describes the type image_file being sent

youtube_id
: optional, *string*, can accept just the id or YouTube short URL from which we will extract the id e.g.,  http://youtu.be/C_S5cXbXe–4

custom_response
: hash, used to create or update data collection fields for Giving Opportunity setup as part of Campaign settings

<div class="api-hash" markdown="1">
campaign_field_id
: optional, *int*, unique id of field 

response
: optional, *string*, data storing for field response
</div>

<a id="update"></a>

Update a Giving Opportunity
-----------------------------------

You can update an existing Giving Opportunity by sending a POST request to the following URI where {id_token} is the unique id for the Giving Opportunity you would like to edit.

     /opportunities/{id_token}

In addition to the authentication and user-agent headers, the following header is also required for POST requests:

     Content-Type: application/json