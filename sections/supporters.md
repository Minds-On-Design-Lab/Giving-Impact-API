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
email_address | string | email address
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

  /supporters

#### Response

```json
{
  error: false,
  supporters: [
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
```


## Retrieve a Supporter

You can retrieve a single supporter by sending a GET request to the URI with the following format:

  /supporters/{id_token}

## Create a Supporter

You can create a new supporter by sending a POST request to the following URI.

    /supporters

In addition to the authentication and user-agent headers, the following header is also required for POST requests:

    Content-Type: application/json

### Example Post Body

```json
{
  "first_name": "Obi Wan",
  "last_name": "Kenobi",
  "email": "jedi@mod-lab.com"
}
```

### Arguments

The following documents the required arguments.

name | required | type/details
------- | ----- | ------------
first_name | | string
last_name | | string
email_address | required | string
street_address | | string
city | | string
state | | string
postal_code | | string
country | required | string
email_address | required | string, email address of donor



## Update an Existing Supporter

You can update an existing supporer by sending a POST request to the following URI where {id_token} is the unique id for the supporter you would like to edit.

     /supporter/{id_token}

In addition to the authentication and user-agent headers, the following header is also required for POST requests:

     Content-Type: application/json
