---
title: LocalStack API Documentation


toc_footers:
  - <a href='#'>Get an Access</a>
  - <a href='http://support.localstack.com'>Get some help</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>
  - <p>&#169; 2014 LocalStack, Inc. San Diego, CA</p>

includes:
  - apiv1
  - apiv2
  - changelog
  - errors
  - terms

search: true
---

# Introduction

Welcome to the LocalStack API documentation! LocalStack is a local business search application which uses social media to provide relavant and interesting results. The API is RESTful and enables adding, updating or delete business listing data on [LocalStack.com](http://LocalStack.com) and it's properties. The API also allows you to check the status and map your business data to our database as well as retrieve all your business listings within our system.

Sample code is currently available as cURL in the dark area to the right. Requests and responses are all in JSON.

The API base url is: **https://api.localstack.com/api/v1/**

The API is versioned, the current version is 1. This is designated in the url path with /v1

If you have any question please visit [our support pages](http://support.localstack.com).


# Authentication

> To set authorization, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl https://api.localstack.com/api/v1/status
  -H "Authorization: Token token=YOUR-ACCESS-TOKEN"
```

> Make sure to replace `YOUR-ACCESS-TOKEN` with your API access key.

LocalStack uses API keys to allow access to the API. You can get an account by contacting us.

The LocalStack API expects for the API key to be included in all API requests to the server. The API key can be passed either as a parameter like the following:

`access_token=YOUR-ACCESS-TOKEN`

Or in a header that looks like the following:

`Authorization: Token token=YOUR-ACCESS-TOKEN`

<aside class="notice">
You must replace `YOUR-ACCESS-TOKEN` with your API key.
</aside>
