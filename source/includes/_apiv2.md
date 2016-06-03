# API V2

## Get LocalStack Listing in JSON

> Request example

```shell
curl "https://api.localstack.com/api/v2/listing/show.json?id=18"
  -H 'Authorization: Token token=YOUR-ACCESS-TOKEN'
```

> The above command returns JSON structured like this:

```json
{
    "response": {
        "status": 200
},
    "listing": {
        "id": 18,
        "url": "http://localstack.com/biz/red-roof-inn-palm-coast-palm-coast-fl/18",
        "name": "Red Roof Inn Palm Coast",
        "address": "10 Kingswood Dr",
        "locality": "Palm Coast",
        "region": "FL",
        "postcode": "32137",
        "tel": "(386) 446-8180",
        "fax": null,
        "website": "http://www.redroof.com",
        "latitude": "29.552629",
        "longitude": "-81.214269",
        "exists": true,
        "score": true,
        "trend": true,
        "media": true,
        "activity": true
    }
}

```

This endpoint retrieves the LocalStack listing.

### HTTP Request

`GET https://api.localstack.com/api/v2/listing/show.json`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
id | true | Localstack ID is required
access_token | true | Access token used to authenticate

Status Type | Description
--------- | -----------
exists | We consider this business to be in existence
score | Social score and data is available for this business
trend | Trending history is available for this business
media | Images and Videos are available for this business
activity | User Activity for Images, Videos, Posts and Tweets are available for this business






## Get Social Score in JSON

> Request example

```shell
curl "https://api.localstack.com/api/v2/score/show.json?id=18"
  -H 'Authorization: Token token=YOUR-ACCESS-TOKEN'
```

> The above command returns JSON structured like this:

```json
{
    "response": {
        "status": 200
},
    "score": {
        "facebook": {
            "score": 38248,
            "historical": 1052631,
            "activity_count": 2,
            "user_count": 1,
            "shares": 0,
            "likes": 38220,
            "checkins": 14,
            "were_here": 14,
            "talking_about": 0,
            "id": "290003480162",
            "src": "https://www.facebook.com/redroofinn/",
            "handle": "redroofinn",
            "shares_historical": 0,
            "likes_historical": 1037389,
            "checkins_historical": 3697,
            "were_here_historical": 3697,
            "talking_about_historical": 7848,
            "name": "Red Roof Inn",
            "description": null
        },
        "google_plus": {
            "score": 1966,
            "historical": 183465,
            "shares": 0,
            "followers": 1,
            "views": 1965,
            "plus_ones": 0,
            "id": "117370405116930240051",
            "src": "https://plus.google.com/117370405116930240051",
            "handle": "117370405116930240051",
            "shares_historical": 0,
            "followers_historical": 779,
            "views_historical": 182686,
            "plus_ones_historical": 0,
            "name": "Red Roof Inn",
            "description": "Red Roof Inn - A Nice Place, at a Nice Price... - Red Roof Inn® was incorporated by founder James R. Trueman in 1972. The brand’s first hotel opened in Columbus, Ohio, with a single room rate of $8.50 in 1973. Today, Red Roof® has nearly 350"
        },
        "twitter": {
            "score": 61,
            "historical": 3259,
            "activity_count": 139,
            "user_count": 90,
            "shares": 0,
            "followers": 61,
            "id": "109568694",
            "src": "https://twitter.com/redroofinn",
            "handle": "redroofinn",
            "shares_historical": 0,
            "tweets_historical": 3150,
            "followers_historical": 3259,
            "following_historical": 521,
            "favorites_historical": 2078,
            "listed_historical": 82,
            "name": "Red Roof Inn",
            "description": "The Official Red Roof Inn Twitter page.",
            "location": "Columbus, OH, USA",
            "joined": "January 2010"
        },
        "instagram": {
            "score": 8,
            "historical": 1911,
            "activity_count": 748,
            "user_count": 288,
            "followers": 8,
            "id": "204436816",
            "src": "https://instagram.com/redroofinn",
            "handle": "redroofinn",
            "media_historical": 436,
            "followers_historical": 1911,
            "following_historical": 549,
            "name": null,
            "description": "Red Roof® is the leader in the economy hotel sector, creating for you the best opportunity to get more out of your travel experience.",
            "webite": "https://www.redroof.com/"
        },
        "like": {
            "score": 0,
            "historical": 0
        },
        "totals": {
            "score": 750,
            "historical": 1241266
        }
    }
}

```

This endpoint retrieves the Social score and data for a LocalStack listing.

### HTTP Request

`GET https://api.localstack.com/api/v2/score/show.json`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
id | true | Localstack ID is required
access_token | true | Access token used to authenticate






## Get Social Trends in JSON

> Request example

```shell
curl "https://api.localstack.com/api/v2/trend/show.json?id=18"
  -H 'Authorization: Token token=YOUR-ACCESS-TOKEN'
```

> The above command returns JSON structured like this:

```json
{
    "response": {
        "status": 200
},
    "trend": {
        "2016-05-29": {
            "facebook_likes": 1037389,
            "facebook_checkins": 3697,
            "facebook_were_here": 0,
            "facebook_talking_about": 0,
            "twitter_followers": 0,
            "google_plus_ones": 0,
            "google_plus_followers": 779,
            "google_plus_views": 182686,
            "instagram_followed_by": 1911,
            "total": 1226462,
            "mean": 1222604.2173913,
            "sd": 4905.00063339553,
            "sats": 0.786499920597354
        }
    }
}

```

This endpoint retrieves up to 30 days of the social trending data for a LocalStack listing.

### HTTP Request

`GET https://api.localstack.com/api/v2/trend/show.json`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
id | true | Localstack ID is required
access_token | true | Access token used to authenticate






## Get Social Media in JSON

> Request example

```shell
curl "https://api.localstack.com/api/v2/media/show.json?id=18"
  -H 'Authorization: Token token=YOUR-ACCESS-TOKEN'
```

> The above command returns JSON structured like this:

```json
{
    "response": {
        "status": 200
    },
    "pagination": {
        "next_page": null,
        "prev_page": null,
        "total_pages": 1,
        "current_page": 1
    },
    "media": [
        {
            "src": "https://www.facebook.com/redroofinn/photos/a.322011875162.155386.290003480162/10153067551575163/",
            "network": "facebook",
            "type": "image",
            "score": 1097,
            "sentiment": 0.999956169,
            "date": 1445458161,
            "image": "https://graph.facebook.com/10153067551575163/picture/?width=400&height=400&type=normal",
            "likes": 941,
            "comments": 93,
            "shares": 63,
            "location": null
        }
    ]
}

```

This endpoint retrieves Images and Videos that are available for a LocalStack listing.

### HTTP Request

`GET https://api.localstack.com/api/v2/media/show.json`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
id | true | Localstack ID is required
access_token | true | Access token used to authenticate
page | false | When not included you'll get a very fast cached first page, when included it'll allow you to more slowly paginate






## Get Social Activity in JSON

> Request example

```shell
curl "https://api.localstack.com/api/v2/activity/show.json?id=18"
  -H 'Authorization: Token token=YOUR-ACCESS-TOKEN'
```

> The above command returns JSON structured like this:

```json
{
    "response": {
        "status": 200
    },
    "pagination": {
        "next_page": null,
        "prev_page": null,
        "total_pages": 1,
        "current_page": 1
    },
    "activity": [
        {
            "src": "https://twitter.com/phrock1055/status/729705621319258112",
            "network": "twitter",
            "type": "image",
            "action": "tweeted",
            "name": "Rock 105.5",
            "sentiment": 0.7243863214,
            "date": 1464609247,
            "user_id": "3187125399",
            "handle": "phrock1055",
            "gender": null,
            "image": "https://pbs.twimg.com/profile_images/730085968196341760/J1KHgqx9_bigger.jpg",
            "likes": 0,
            "shares": 0,
            "location": null
        }
    ]
}

```

This endpoint retrieves User Activity for Images, Videos, Posts and Tweets that are available for a LocalStack listing.

### HTTP Request

`GET https://api.localstack.com/api/v2/activity/show.json`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
id | true | Localstack ID is required
access_token | true | Access token used to authenticate
page | false | When not included you'll get a very fast cached first page, when included it'll allow you to more slowly paginate






## Get Listing by Factual ID in JSON

> Request example

```shell
curl "https://api.localstack.com/api/v2/factual/show.json?factual_id=99db4cc4-875c-4238-8b94-8f58a11bdbc2"
  -H 'Authorization: Token token=YOUR-ACCESS-TOKEN'
```

> The above command returns JSON structured like this:

```json
{
    "response": {
        "status": 200
    },
    "factual": {
        "id": 18,
        "factual_id": "99db4cc4-875c-4238-8b94-8f58a11bdbc2",
        "exists": true,
        "score": true,
        "trend": true,
        "media": true,
        "activity": true
    }
}

```

This endpoint retrieves the LocalStack listing.

### HTTP Request

`GET https://api.localstack.com/api/v2/factual/show.json`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
id or factual_id | true | Localstack or Factual ID is required
access_token | true | Access token used to authenticate

Status Type | Description
--------- | -----------
exists | We consider this business to be in existence
score | Social score and data is available for this business
trend | Trending history is available for this business
media | Images and Videos are available for this business
activity | User Activity for Images, Videos, Posts and Tweets are available for this business
