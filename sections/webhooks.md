# Webhooks

- [Overview](#overview)
- [Authentication](#authentication)
- [Hook Validation](#hook-validation)
- [Hook Events](#hook-events)
- [Event Returned Data](#event-returned-data)
- [Get a list of Webhook Subscriptions for Your Account](#get-a-list-of-webhook-subscriptions-for-your-account)
- [Create a New Hook Subscription](#create-a-new-hook-subscription)
- [Get a Specific Hook](#get-a-specific-hook)
- [Update an Exisitng Hook](#update-an-existing-hook)
- [Delete a Hook](#delete-a-hook)
- [Hook Failures](#hook-failures)

## Overview

Webhooks provides a means for you to receive automated and systemic updates when certain events in Giving Impact(TM) happen. Webhooks compliment the API in that an API is where you go to make requests to get, create, and change data. Webhooks reaches out to you with critical data when certain events you care about happen. For example you can subscribe to a hook that will send you complete donation data every time a new donation is created.

This is a powerful integration tool allowing you further control over your data.

When you subscribe to a webhook you provide a URL to an endpoint of your choosing. This URL will be crafted by you to receive incoming data from the subscribed hook and will be prepared to process it.

The following outlines the process of working with Giving Impact's Webhooks and details the specific hooks you can subscribe to.

## Authentication

All requests to the Webhooks API require authentication using a valid API Key for the account.

     X-GI-Authorization: {api-key-string}

## Hook Validation

Hooks must be validated before they're activated. Validation is a process of creating a new hook and then negotiation the establishing and confirmation of a unique token.

1. Account creates new hook
2. Webhook API responds to confirm receipt of request
3. Webhook API then posts an exchange token to provided Account endpoint
4. Account endpoint receives exchange token and POSTs to API with validated token
5. Hook API activates event

In practice it looks like this:

1. First, client creates new hook:

         POST hook/subscriptions HTTP/1.1
         X-GI-Authorization: {api-key-string}
         Content-Type: application/json
         {
             "event":    "donation.create",
             "url":      "http://example.com/foo"
         }

2. and the API responds with:

         HTTP/1.1 200 OK
         Connection: close
         Content-Type: application/json;charset=utf-8
         {
             "isError": false,
             "hook": {
                 "id":       "ABC123",
                 "event":    "donation.create",
                 "url":      "http://example.com/foo",
                 "status":   "inactive",
                 "last_run": 0
             }
         }

3. Next, the API will ping the provided endpoint with the hook's hash and an exchange token with the `hook.register` event:

         POST {{your_subscribed_endpoint}} HTTP/1.1
         Content-Type: application/json
         {
             "event":    "hook.register",
             "payload":  {
                 "hook":     {
                     "id":       "ABC123",
                     "token":    "A-VERY-LONG-STRING"
                 }
             }
         }

4. The client endpoint then calculates a MD5 hash of the provided `token` and their API key. The newly created token is POSTed back to the webhook API:

         POST hook/subscriptions/ABC123 HTTP/1.1
         X-GI-Authorization: {api-key-string}
         Content-Type: application/json
         {
             "verification":    MYNEWCOMBINEDTOKEN
         }

5. The API will validate the token and activate the hook:

         HTTP/1.1 200 OK
         Connection: close
         Content-Type: application/json;charset=utf-8
         {
             "isError": false,
             "hook": {
                 "id":       "ABC123",
                 "event":    "donation.create",
                 "url":      "http://example.com/foo",
                 "status":   "active",
                 "last_run": 0
             }
         }


## Hook Events

The following events are supported.

### Administrative

* hook.register

### Donations

* donation.create
* donation.edit

### Giving Opportunities

* opportunity.create
* opportunity.edit

Each event will return data for the appropriate object. For details of returned data please review the docs for the appropriate object.

## Event Returned Data

Data from events is packaged as follows:

    POST {your_subscribed_endpoint} HTTP/1.1
    Content-Type: application/json
    {
        "event":    "hook.register",
        "payload":  {
            ...
            }
        }
    }

Within the `payload` element will be the specific object the event is related to such as a `donation`. That object will include all related data. For details about the specific object and data returned refer to that object's API documentation page.

<a id="list"></a>

## Get a list of Webhook Subscriptions for Your Account

You can retrieve a list of subscriptions by sending a GET request to the URI with the following format:

    hook/subscriptions

### Response

    HTTP/1.1 200 OK
    Connection: close
    Content-Type: application/json;charset=utf-8
    {
        "isError": false,
        "hooks": [
            {
                "id":       "STRING",
                "event":    "STRING",
                "url":      "STRING",
                "status":   "ENUM('active','inactive')",
                "last_run": "STRING"
            },
            ...
        ]
    }

<a id="create"></a>

## Create a New Hook Subscription

To create a new hook send a POST request to the URI with the following format:

    hook/subscriptions

### Required Fields

- event
- url

### Example POST

    POST hook/subscriptions HTTP/1.1
    X-GI-Authorization: {api-key-string}
    Content-Type: application/json
    {
        "event":    "donation.create",
        "url":      "http://example.com/foo"
    }

### Response

    HTTP/1.1 200 OK
    Connection: close
    Content-Type: application/json;charset=utf-8
    {
        "isError": false,
        "hook": {
            "id":       "ABC123",
            "event":    "donation.create",
            "url":      "http://example.com/foo",
            "status":   "inactive",
            "last_run": 0
        }
    }

*Note that the hook is disabled and must be activated*

<a id="get_hook"></a>

## Get a Specific Hook

You can retrieve a specific hook by sending a GET request to the URI with the following format:

    hook/subscriptions/{id}

### Response

    HTTP/1.1 200 OK
    Connection: close
    Content-Type: application/json;charset=utf-8
    {
        "isError": false,
        "hook": {
            "id":       "ABC123",
            "event":    "donation.create",
            "url":      "http://example.com/foo",
            "status":   "true",
            "last_run": 0
        }
    }

<a id="update_hook"></a>

## Update an Existing Hook

To update an existing hook send a POST request to the URI with the following format:

    hook/subscriptions/{id}

### Example POST

Update or validate a webhook. Passing a single `token` value will validate a hook, all other requests will update the hook

    POST hook/subscriptions/{id} HTTP/1.1
    X-GI-Authorization: {api-key-string}
    Content-Type: application/json
    {
        "event":    "donation.create",
        "url":      "http://example.com/bar"
    }

### Response

    HTTP/1.1 200 OK
    Connection: close
    Content-Type: application/json;charset=utf-8
    {
        "isError": false,
        "hook": {
            "id":       "ABC123",
            "event":    "donation.create",
            "url":      "http://example.com/foo",
            "status":   "true",
            "last_run": 0
        }
    }

<a id="delete_hook"></a>

## Delete a Hook

To delete a hook send a DELETE request to the URI with the following format:

    hook/subscriptions/{id}

### Example DELETE

    DELETE hook/subscriptions/{id} HTTP/1.1
    X-GI-Authorization: {api-key-string}
    Content-Type: application/json

### Example Response

    HTTP/1.1 200 OK
    Connection: close
    Content-Type: application/json;charset=utf-8
    {
        "isError": false,
        "status": "ok"
    }

<a id="failures"></a>

## Hook Failures

Imagine your URL endpoint becomes unavailible for a time, what happens when events fire and we can't connect to make a successful call?

In the event of a failed hook request, our service will:

1. Retry after 5 seconds
2. Retry again after another 10 seconds
3. Retry again after another 30 seconds
4. Retry again after another 60 seconds
5. Retry again every 60 seconds for 10 minutes
6. Retry again every 10 minutes for 24 hours

After 24 hours, the hook will be automatically disabled, but not deleted. If/when the hook call does succeed again, the retry queue is reset. For example:

1. Your hook end point goes down for an hour
2. Hook system tries contacting you for an hour, eventually getting to step 5 above
3. Hook system succeeds in contacting your endpoint
4. Your endpoint goes down again later that day
5. Hook system starts all over at step 1 above again for the next hook call
