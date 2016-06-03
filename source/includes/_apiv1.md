# API V1

## Listing Data Types

> Sample JSON Payload:

```json
{
  "status": "AVAILABLE",
  "listing_id": "f76ae9ceb01cf2904fe2",
  "mojo_id": "11079728",
  "mojo_url": "https://www.localstack.com/biz/instant-phones-phoenix-az/11079728",
  "name": "Instant Phones",
  "description": null,
  "address": "2415 E Thomas Rd",
  "locality": "Pheonix",
  "region": "AZ",
  "postcode": "85016",
  "tel": "(602) 224-9582",
  "website": "http://www.mycricket.com/",
  "longitude": "-112.10158",
  "latitude": "33.643668",
  "facebook_id": "111664078919577",
  "twitter_id": "cricketnation",
  "google_plus_id": null,
  "instagram_id": "cricketnation",
  "omit_address": false,
  "hours": {
      "monday": [
        [
          "8:00",
          "16:00"
        ]
      ]
    },
  "category_ids": [
      "467"
    ],
  "logo_url": null,
  "photo_urls": [],
  "video_urls": [],
  "offer_message": null,
  "offer_url": null,
  "attribution_logo": {
      "description": "Company",
      "url": "http://www.company.com/attribution/logo.png",
      "width": 100,
      "height": 20
    },
  "attribution_url": "http://www.company.com",
  "updated_at": "2014-11-27T11:35:27.364Z"
}

```

Business listings are made up of different pieces of data. These are the excepted base record data for a business. These should be sent in the JSON payload. These are all optional except where requests require a particular parameter. You may also add in any data that is not included specifically here, label the data type appropriatly, we will accept any data you would like to send.

### Status Types

Status Type | Description
--------- | -----------
AVAILABLE | This listing is not currently a claimed listing, it may be successfully claimed by you.
ACTIVE | This listing is fully activated and live on LocalStack.com.
SUPPRESSED | The listing is suppressed, which means it should not appear in our search results or have a detail page.
BLOCKED | The listing has an existing relationship with another partner and may not be controlled by you.

### Data Types

Data Type | Description
--------- | -----------
status | Contains either AVAILABLE, ACTIVE, SUPPRESSED or BLOCKED status
listing_id | Your unique identifier for the listing, used for adding or deleting a record
mojo_id | Claims a Business based on mojo_id, will automap or create new listing when not included
mojo_url | URL for LocalStack listing
name | Name of the business
description | Description of the business
address | Address of the business
address_extended | Second address of the business if there is one
locality | City where the business is located
region | State in which the business is located, should be 2 character abreviation
postcode | Postal code where the business is located, should be a minimum 5 digits
tel | Telephone number of the business, should be 10 digits
fax | Fax number of the business, should be 10 digits
website |  URL for the business, include http://
email | Email address for the business
longitude | Longitude of the business location
latitude | Latitude of the business location
facebook_id | The Facebook ID or the name of the page for the business
twitter_id | Twitter username for the business, without the @ symbol
google_plus_id | The Google Plus ID or the name used for the page of the business
instagram_id | The Instgram ID or the username for the business listing
omit_address | Boolean for omitting the address from the listing (default: false)
hours | The Hours a business is open or closed represented by a hash of multi dimensional arrays or do not include days where business is completely closed.
category_ids | LocalStack Category ID's that you want business to be listed under array (max: 3)
logo_url | URL for the listing logo, must be a minimum of 150x150 pixels
photo_urls | Array of URLs for the listing photos, must all be a minimum of 150x150 pixels
video_urls | Array of URLs for the listing videos, must be either YouTube or Vimeo links
offer_message | Special Offer or Coupon Message used as a link on the listing page
offer_url | Special Offer or Coupon URL used as a link on the listing page
attribution_logo | Partner attribution logo hash with description, width, height and a url that also supports https
attribution_url | Partner attribution url
updated_at | When the listing was last updated

## Getting Started Workflow

There are many ways and uses for the API. Here are the major typical workflows:

1) [Find Right Category ID](#get-categories-in-json) - You'll first want to grab a list of our category ID's before getting started.

2) [Search for listings](#get-a-search-for-listings-in-json) - We recommend when searching using: Name, Address, Latitude, Longitude and Phone number.

3) [Get a listing detail](#get-a-listing) - Verify the listings status and make sure that it is Available to be claimed.

4) [Post partner listings](#post-a-new-partner-listing) - Push all your listings into our database with your listing ID and the Mojo_ID of the listing you want to claim ownership for.

4.A) [Post a suppress listing](#post-suppress-a-listing) - If there are duplicates or other issues with listings in our database then supress them.

4.B) [Add a partner listing](#post-a-new-partner-listing) - If you have verified there is no match to a search result, Post a partner listing without a Mojo_ID and it will be added.

4.C) [Update partner listing](#update-a-partner-listing) - If you have claimed a listing and the status is active then you can update it at anytime and any parameters passed will be updated.

5) [Get partner listings](#get-partner-listings-in-json) - Lastly this will give you all your listings and the status of those listins in our database.


## Get Status

> Request example

```shell
curl "https://api.localstack.com/api/v1/status"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "response": {
    "status": 200
  },
  "api_status": "published",
  "partner": "Company Name",
  "total_listings": 12000,
  "mapped_listings": 600,
  "claimed_listings": 600
}
```

Check the status of the inserted businesses and the current total businesses mapped.

### HTTP Request

`GET https://api.localstack.com/api/v1/status`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate


### Status Types

Status Type | Description
--------- | -----------
api_status | Tells you development status of api from alpha to beta to finally published
partner | Your Partner company name
total_listings | Total number of listings we or you have imported through our Partner endpoints
mapped_listings | Total number of your listings that we've mapped to ours
claimed_listings | Total number of our listings that you have claimed



## Get Partner Listings in JSON

> Request example

```shell
curl "https://api.localstack.com/api/v1/partner/listings"
  -H 'Authorization: Token token=YOUR-ACCESS-TOKEN'
```

> The above command returns JSON structured like this:

```json
{
  "response": {
    "status": 200
  },
  "listings": [
    {
      "status": "ACTIVE",
      "listing_id": "f76ae9ceb01cf2904fe2",
      "mojo_id": "11079728",
      "mojo_url": "https://www.localstack.com/biz/instant-phones-phoenix-az/11079728",
      "name": "Instant Phones",
      "description": null,
      "address": "2415 E Thomas Rd",
      "locality": "Pheonix",
      "region": "AZ",
      "postcode": "85016",
      "tel": "(602) 224-9582",
      "website": "http://www.mycricket.com/",
      "longitude": "-112.10158",
      "latitude": "33.643668",
      "facebook_id": "111664078919577",
      "twitter_id": "cricketnation",
      "google_plus_id": null,
      "instagram_id": "cricketnation",
      "omit_address": false,
      "hours": {
          "monday": [
            [
              "8:00",
              "16:00"
            ]
          ]
        },
      "category_ids": [
          "467"
        ],
      "logo_url": null,
      "photo_urls": [],
      "video_urls": [],
      "offer_message": null,
      "offer_url": null,
      "menu_url": null,
      "attribution_logo": {
          "description": "Company",
          "url": "http://www.company.com/attribution/logo.png",
          "width": 100,
          "height": 20
        },
      "attribution_url": "http://www.company.com",
      "updated_at": "2014-11-27T11:35:27.364Z"
    }
  ]
}

```

This endpoint retrieves all your existing business listings.

### HTTP Request

`GET https://api.localstack.com/api/v1/partner/listings`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate

Status Type | Description
--------- | -----------
AVAILABLE | This listing is not currently a claimed listing, it may be successfully claimed by you.
ACTIVE | This listing is fully activated and live on LocalStack.com.
SUPPRESSED | The listing is suppressed, which means it should not appear in our search results or have a detail page.
BLOCKED | The listing has an existing relationship with another partner and may not be controlled by you.




## Get Partner Listings in CSV

> Request example

```shell
curl "https://api.localstack.com/api/v1/partner/listings/csv"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN" >> Listings.csv
```

> The above command returns CSV structured like this:

```csv
status, listing_id, mojo_id, mojo_url, name, address, locality, region, postcode, tel, website, longitude, latitude, facebook_id, twitter_id, google_plus_id, instagram_id, mapped, claimed, omit_address, updated_at
ACTIVE, f76ae9ceb01cf2904fe2, 11079728, https://www.localstack.com/biz/instant-phones-phoenix-az/11079728, Instant Phones, 2415 E Thomas Rd, Pheonix, AZ, 85016, (602) 224-9582, http://www.mycricket.com/, -112.10158,33.643668, 111664078919577, cricketnation, , cricketnation, false, false, false, 2014-11-27T11:35:27.364Z
```

This endpoint retrieves all your existing business listings.

### HTTP Request

`GET https://api.localstack.com/api/v1/partner/listings/csv`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate

Status Type | Description
--------- | -----------
AVAILABLE | This listing is not currently a claimed listing, it may be successfully claimed by you.
ACTIVE | This listing is fully activated and live on LocalStack.com.
SUPPRESSED | The listing is suppressed, which means it should not appear in our search results or have a detail page.
BLOCKED | The listing has an existing relationship with another partner and may not be controlled by you.





## Get a Partner Listing

> Request example

```shell
curl "https://api.localstack.com/api/v1/partner/listing/7d373c1da40cbfc3f165"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "response": {
    "status": 200
  },
  "listing": {
    "status": "ACTIVE",
    "listing_id": "f76ae9ceb01cf2904fe2",
    "mojo_id": "11079728",
    "mojo_url": "https://www.localstack.com/biz/instant-phones-phoenix-az/11079728",
    "name": "Instant Phones",
    "description": null,
    "address": "2415 E Thomas Rd",
    "locality": "Pheonix",
    "region": "AZ",
    "postcode": "85016",
    "tel": "(602) 224-9582",
    "website": "http://www.mycricket.com/",
    "longitude": "-112.10158",
    "latitude": "33.643668",
    "facebook_id": "111664078919577",
    "twitter_id": "cricketnation",
    "google_plus_id": null,
    "instagram_id": "cricketnation",
    "omit_address": false,
    "hours": {
        "monday": [
          [
            "8:00",
            "16:00"
          ]
        ]
      },
    "category_ids": [
        "467"
      ],
    "logo_url": null,
    "photo_urls": [],
    "video_urls": [],
    "offer_message": null,
    "offer_url": null,
    "menu_url": null,
    "attribution_logo": {
        "description": "Company",
        "url": "http://www.company.com/attribution/logo.png",
        "width": 100,
        "height": 20
      },
    "attribution_url": "http://www.company.com",
    "updated_at": "2014-11-27T11:35:27.364Z"
  }
}
```

This endpoint retrieves a specific business listings.

### HTTP Request

`GET https://api.localstack.com/api/v1/partner/listing/:LISTING_ID`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate
:LISTING_ID| true | Your ID for the specific business listing

<aside class="notice">
You must replace `:LISTING_ID` with your business listing id.
</aside>

### Status Types

Status Type | Description
--------- | -----------
AVAILABLE | This listing is not currently a claimed listing, it may be successfully claimed by you.
ACTIVE | This listing is fully activated and live on LocalStack.com.
SUPPRESSED | The listing is suppressed, which means it should not appear in our search results or have a detail page.
BLOCKED | The listing has an existing relationship with another partner and may not be controlled by you.





## Post a New Partner Listing

> Request example

```shell
curl "https://api.localstack.com/api/v1/partner/listing/7d373c1da40cbfc3f165"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"
  -H "Content-Type: application/json"
  -X POST -d '{"mojo_id": 201702, "name": "Piety Hill Cottages", "address": "523 Sacramento St", "tel": "(555) 555-5555", "locality": "Nevada City", "region": "CA", "postcode":"95959", "latitude": "47.288845", "longitude": "-101.0308", "hours": {"sunday":[["closed"]], "monday": [["8:00","16:00"]]}, "category_ids": [467]}'

```

> The above command returns JSON structured like this if it gets claimed:

```json
{
  "response": {
    "status": 200
  },
  "listing_status": {
    "status": "LIVE"
  },
  "listing": {
    "listing_id": "7d373c1da40cbfc3f165",
    "mojo_id": "201702",
    "mojo_url": "https://www.localstack.com/biz/piety-hill-cottages-phoenix-az/201702"
  }
}
```

> The above command returns JSON structured like this if it's already claimed:

```json
{
  "response": {
    "status": 422
  },
  "listing_status": {
    "status": "BLOCKED"
  },
  "listing": {
    "listing_id": "7d373c1da40cbfc3f165",
    "mojo_id": "201702",
    "mojo_url": "https://www.localstack.com/biz/piety-hill-cottages-phoenix-az/201702"
  }
}
```

> The above command returns JSON structured like this if it's validations are rejected:

```json
{
  "response": {
    "status": 422
  },
  "listing_status": {
    "status": "REJECTED"
  },
  "listing": {
    "listing_id": "7d373c1da40cbfc3f165",
    "mojo_id": "201702",
    "mojo_url": "https://www.localstack.com/biz/piety-hill-cottages-phoenix-az/201702"
  },
  "error": {
    "messages": [
      {
        "message": "Validation failed: Postcode can't be blank"
      }
    ]
  }
}
```

This endpoint is used to post a new business listings to LocalStack.

### HTTP Request

`POST https://api.localstack.com/api/v1/partner/listing/:LISTING_ID`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate
:LISTING_ID| true | Your ID for the specific business listing

<aside class="notice">
You must replace `:LISTING_ID` with your business listings id.
</aside>

### Status Types

Status Type | Description
--------- | -----------
LIVE | The Listing added or mapped is fully activated and live on LocalStack.com.
REJECTED | The Listing did not pass our validation and description of the issue will be stated.
BLOCKED | You cannot create the Listing and description of the issue will be stated.

### Available JSON Listing Values

Listing Value | required | Description
--------- | ----------- | -----------
listing_id | true | Your unique identifier for the listing, used for adding or deleting a record
mojo_id | false | Claims a Business based on mojo_id, will automap or create new listing when not included
name | true | Name of the business
description | false | Description of the business
address | true | Address of the business
address_extended | false | Second address of the business if there is one
locality | true | City where the business is located
region | true | State in which the business is located, should be 2 character abreviation
postcode | true | Postal code where the business is located, should be a minimum 5 digits
tel | false | Telephone number of the business, should be 10 digits
fax | false | Fax number of the business, should be 10 digits
website | false | URL for the business, include http://
email | false | Email address for the business
longitude | true | Longitude of the business location
latitude | true | Latitude of the business location
facebook_id | false | The Facebook ID or the name of the page for the business
twitter_id | false | Twitter username for the business, without the @ symbol
google_plus_id | false | The Google Plus ID or the name used for the page of the business
instagram_id | false | The Instgram ID or the username for the business listing
omit_address | false | Boolean for omitting the address from the listing (default: false)
hours | false | The Hours a business is open or closed represented by a hash of multi dimensional arrays or do not include days where business is completely closed.
category_ids | true | LocalStack Category ID's that you want business to be listed under array (max: 3)
logo_url | false | URL for the listing logo, must be a minimum of 150x150 pixels
photo_urls | false | Array of URLs for the listing photos, must all be a minimum of 150x150 pixels
video_urls | false | Array of URLs for the listing videos, must be either YouTube or Vimeo links
offer_message | false | Special Offer or Coupon Message used as a link on the listing page
offer_url | false | Special Offer or Coupon URL used as a link on the listing page
menu_url | false | Menu URL used as a link on the listing page
attribution_logo | false | Partner attribution logo hash with description, width, height and a url that also supports https
attribution_url | false | Partner attribution url



## Update a Partner Listing

> Request example

```shell
curl "https://api.localstack.com/api/v1/partner/listing/7d373c1da40cbfc3f165"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"
  -H "Content-Type: application/json"
  -X PUT -d '{"address": "523 Sacramento Streeet", "tel": "(800) 555-5555", "hours": {"sunday":[["closed"]], "monday": [["8:00","16:00"]]}}'

```

> The above command returns JSON structured like this if it gets claimed:

```json
{
  "response": {
    "status": 200
  },
  "listing_status": {
    "status": "LIVE"
  },
  "listing": {
    "listing_id": "7d373c1da40cbfc3f165",
    "mojo_id": "201702",
    "mojo_url": "https://www.localstack.com/biz/piety-hill-cottages-phoenix-az/201702"
  }
}
```

> The above command returns JSON structured like this if it's already claimed:

```json
{
  "response": {
    "status": 422
  },
  "listing_status": {
    "status": "BLOCKED"
  },
  "listing": {
    "listing_id": "7d373c1da40cbfc3f165",
    "mojo_id": "201702",
    "mojo_url": "https://www.localstack.com/biz/piety-hill-cottages-phoenix-az/201702"
  }
}
```

This endpoint is used to put updated data for an existing business listing into LocalStack.

### HTTP Request

`PUT https://api.localstack.com/api/v1/partner/listing/:LISTING_ID`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate
:LISTING_ID| true | Your ID for the specific business listing being updated

<aside class="notice">
You must replace `:LISTING_ID` with your business listings id.
</aside>

### Status Types

Status Type | Description
--------- | -----------
LIVE | The Listing added or mapped is fully activated and live on LocalStack.com.
REJECTED | The Listing did not pass our validation and description of the issue will be stated.
BLOCKED | You cannot create the Listing and description of the issue will be stated.

### Available JSON Listing Values

Listing Value | Description
--------- | -----------
listing_id | Your unique identifier for the listing, used for adding or deleting a record
mojo_id | Claims a Business based on mojo_id, will automap or create new listing when not included
name | Name of the business
description | Description of the business
address | Address of the business
address_extended | Second address of the business if there is one
locality | City where the business is located
region | State in which the business is located, should be 2 character abreviation
postcode | Postal code where the business is located, should be a minimum 5 digits
tel | Telephone number of the business, should be 10 digits
fax | Fax number of the business, should be 10 digits
website | URL for the business, include http://
email | Email address for the business
longitude | Longitude of the business location
latitude | Latitude of the business location
facebook_id  | The Facebook ID or the name of the page for the business
twitter_id | Twitter username for the business, without the @ symbol
google_plus_id | The Google Plus ID or the name used for the page of the business
instagram_id | The Instgram ID or the username for the business listing
omit_address | Boolean for omitting the address from the listing (default: false)
hours | The Hours a business is open or closed represented by a hash of multi dimensional arrays or do not include days where business is completely closed.
category_ids | LocalStack Category ID's that you want business to be listed under array (max: 3)
logo_url | URL for the listing logo, must be a minimum of 150x150 pixels
photo_urls | Array of URLs for the listing photos, must all be a minimum of 150x150 pixels
video_urls | Array of URLs for the listing videos, must be either YouTube or Vimeo links
offer_message | Special Offer or Coupon Message used as a link on the listing page
offer_url | Special Offer or Coupon URL used as a link on the listing page
menu_url | false | Menu URL used as a link on the listing page
attribution_logo | Partner attribution logo hash with description, width, height and a url that also supports https
attribution_url | Partner attribution url


## Delete a Partner Listing

> Request example

```shell
curl "https://api.localstack.com/api/v1/partner/listing/7d373c1da40cbfc3f165"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"

```

> The above command returns JSON structured like this:

```json
{
  "response": {
    "status": 200
  },
  "success": true
}
```

This endpoint is used to delete an existing business listing from LocalStack.

### HTTP Request

`DELETE https://api.localstack.com/api/v1/partner/listing/:LISTING_ID`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate
:LISTING_ID| true | Your ID for the specific business listing being deleted

<aside class="notice">
You must replace `:LISTING_ID` with your business listings id.
</aside>





## Get Categories in JSON

> Request example

```shell
curl "https://api.localstack.com/api/v1/categories"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "response": {
    "status": 200
  },
  "categories": [
    {
      "category_id": 2,
      "parent_category_id": 1,
      "category_level": 1,
      "title": "Automotive",
      "naic_code": null,
      "sic_code": null
    }
  ]
}
```

Check the status of the inserted businesses and the current total businesses mapped.

### HTTP Request

`GET https://api.localstack.com/api/v1/categories`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate




## Get Categories in CSV

> Request example

```shell
curl "https://api.localstack.com/api/v1/categories/csv"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN" >> Categories.csv
```

> The above command returns CSV structured like this:

```csv
category_id, parent_category_id, category_level, title, naic_code, sic_code
2,1,1,Automotive,,
```

Check the status of the inserted businesses and the current total businesses mapped.

### HTTP Request

`GET https://api.localstack.com/api/v1/categories/csv`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate





## Get a Search for Listings in JSON

> Request example

```shell
curl "https://api.localstack.com/api/v1/listings/search?name=Instant+Phones&locality=Pheonix&region=AZ"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "response": {
    "status": 200
  },
  "listings": [
    {
      "status": "AVAILABLE",
      "mojo_id": "11079728",
      "mojo_url": "https://www.localstack.com/biz/instant-phones-phoenix-az/11079728",
      "name": "Instant Phones",
      "description": null,
      "address": "2415 E Thomas Rd",
      "locality": "Pheonix",
      "region": "AZ",
      "postcode": "85016",
      "tel": "(602) 224-9582",
      "website": "http://www.mycricket.com/",
      "longitude": "-112.10158",
      "latitude": "33.643668",
      "omit_address": false,
      "hours": {
          "monday": [
            [
              "8:00",
              "16:00"
            ]
          ]
        },
      "category_ids": [
          "467"
        ],
      "logo_url": null,
      "photo_urls": [],
      "video_urls": [],
      "offer_message": null,
      "offer_url": null,
      "menu_url": null,
      "attribution_logo": {
          "description": "Company",
          "url": "http://www.company.com/attribution/logo.png",
          "width": 100,
          "height": 20
        },
      "attribution_url": "http://www.company.com",
      "updated_at": "2014-11-27T11:35:27.364Z"
    }
  ]
}
```

This endpoint allows you to search the LocalStack database like you would do on the site but with more specific attributes like Name, Address, Latitude, Longitude and Phone number.

### HTTP Request

`GET https://api.localstack.com/api/v1/listings/search`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate
results | false | Number of results to return (default returns one listing)
name | false | Name of the business
address | false | Address of the business
address_extended | false | Second address of the business if there is one
locality | false | City where the business is located
region | false | State in which the business is located, should be 2 character abreviation
postcode | false | Postal code where the business is located, should be a minimum 5 digits
tel | false | Telephone number of the business, should be 10 digits
website | false | URL for the business, include http://
longitude | false | Longitude of the business location
latitude | false | Latitude of the business location

Status Type | Description
--------- | -----------
AVAILABLE | This listing is not currently a claimed listing, it may be successfully claimed by you.
ACTIVE | This listing is fully activated and live on LocalStack.com.
SUPPRESSED | The listing is suppressed, which means it should not appear in our search results or have a detail page.
BLOCKED | The listing has an existing relationship with another partner and may not be controlled by you.




## Get a Listing

> Request example

```shell
curl "https://api.localstack.com/api/v1/listing/11079728"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "response": {
    "status": 200
  },
  "listing": {
    "status": "AVAILABLE",
    "mojo_id": "11079728",
    "mojo_url": "https://www.localstack.com/biz/instant-phones-phoenix-az/11079728",
    "name": "Instant Phones",
    "description": null,
    "address": "2415 E Thomas Rd",
    "locality": "Pheonix",
    "region": "AZ",
    "postcode": "85016",
    "tel": "(602) 224-9582",
    "website": "http://www.mycricket.com/",
    "longitude": "-112.10158",
    "latitude": "33.643668",
    "facebook_id": "111664078919577",
    "twitter_id": "cricketnation",
    "google_plus_id": null,
    "instagram_id": "cricketnation",
    "status": "AVAILABLE",
    "omit_address": false,
    "hours": {
        "monday": [
          [
            "8:00",
            "16:00"
          ]
        ]
      },
    "category_ids": [
        "467"
      ],
    "logo_url": null,
    "photo_urls": [],
    "video_urls": [],
    "offer_message": null,
    "offer_url": null,
    "menu_url": null,
    "attribution_logo": {
        "description": "Company",
        "url": "http://www.company.com/attribution/logo.png",
        "width": 100,
        "height": 20
      },
    "attribution_url": "http://www.company.com",
    "updated_at": "2014-11-27T11:35:27.364Z"
  }
}
```

This endpoint retrieves a specific business listings.

### HTTP Request

`GET https://api.localstack.com/api/v1/listing/:MOJO_ID`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate
:MOJO_ID| true | Your ID for the specific business listing

<aside class="notice">
You must replace `:MOJO_ID` with your business listing id.
</aside>

Status Type | Description
--------- | -----------
AVAILABLE | This listing is not currently a claimed listing, it may be successfully claimed by you.
ACTIVE | This listing is fully activated and live on LocalStack.com.
SUPPRESSED | The listing is suppressed, which means it should not appear in our search results or have a detail page.
BLOCKED | The listing has an existing relationship with another partner and may not be controlled by you.





## Get a Listing by Factual ID

> Request example

```shell
curl "https://api.localstack.com/api/v1/listing/693acfb0-a323-44c5-8aa1-75baf9f99f3a/factual"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "response": {
    "status": 200
  },
  "listing": {
    "mojo_id": "11079728",
    "mojo_url": "https://www.localstack.com/biz/instant-phones-phoenix-az/11079728",
    "name": "Instant Phones",
    "address": "2415 E Thomas Rd",
    "locality": "Pheonix",
    "region": "AZ"
  }
}
```

This endpoint retrieves a specific business listings by the Factual ID.

### HTTP Request

`GET https://api.localstack.com/api/v1/listing/:FACTUAL_LISTING_ID/factual`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate
:FACTUAL_LISTING_ID| true | Factual ID for the specific business listing

<aside class="notice">
You must replace `:FACTUAL_LISTING_ID` with the business listings Factual id.
</aside>




## Post Suppress a Listing

> Request examples

```shell
curl "https://api.localstack.com/api/v1/listing/11079728/suppress?reason=closed"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"
  -X POST

```

```shell
curl "https://api.localstack.com/api/v1/listing/11079728/suppress/4279039?reason=duplicate"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"
  -X POST

```

> The above command returns JSON structured like this:

```json
{
  "response": {
    "status": 200
  },
  "success": true
}
```

This endpoint is used to to suppress a duplicate or invalid listings on LocalStack. If a listing is SUPPRESSed, we will remove the listing from our site's search results. If a CANONICALLISTING_MOJO_ID is included in the path then a redirect is setup with 301 permenant redirection to the correct listing.

### HTTP Request

`POST https://api.localstack.com/api/v1/listing/:MOJO_ID/suppress`

`POST https://api.localstack.com/api/v1/listing/:MOJO_ID/suppress/:CANONICALLISTING_MOJO_ID`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate
reason | false | Your Reason for wanting to suppress the listing (limit of 255 characters)
:MOJO_ID| true | Our Mojo ID for the specific business listing being redirected from
:CANONICALLISTING_MOJO_ID| false | The Mojo ID for the destination business listing being redirected to


<aside class="notice">
You must replace `:MOJO_ID` with your duplicate business Mojo ID. You can also replace `:CANONICALLISTING_MOJO_ID` for the Mojo ID of the business you wish to redirect to.
</aside>





## Post Unsuppress a Listing

> Request example

```shell
curl "https://api.localstack.com/api/v1/listing/11079728/unsuppress"
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"
  -X POST

```

> The above command returns JSON structured like this:

```json
{
  "response": {
    "status": 200
  },
  "success": true
}
```

This endpoint is used to remove a redirect or suppression for a business listings to LocalStack. You need to be the one who originally suppressed the listing in order to unsupress it.

### HTTP Request

`POST https://api.localstack.com/api/v1/listing/:MOJO_ID/unsuppress`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
access_token | true | Access token used to authenticate
:MOJO_ID| true | Our Mojo ID for the specific business listing that needs to no longer be redirected


<aside class="notice">
You must replace `:MOJO_ID` with your non duplicate business Mojo id.
</aside>
