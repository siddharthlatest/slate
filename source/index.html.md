---
title: Appbase.io API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript
  - go
  - ruby
  - python
  - java

toc_footers:
  - <a href='https://dashboard.appbase.io'>Sign Up for a Developer Account</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the appbase.io API! appbase.io is a streaming database service built around Elasticsearch. You can use it to build reactive apps, realtime maps, blazing fast search and recommendations, chats, feeds, IoT apps.

![appbase.io in one image](https://i.imgur.com/iJpqtks.png?1)

A client device can subscribe to appbase.io for continuous queries and data updates. appbase.io keeps the connection alive and streams updates as JSON everytime there is a relevant change.

We offer a HTTP based RESTful API service. Our streaming APIs work via HTTP, and we support websockets protocol as well for browsers and native mobile environments.

We support a Javascript SDK that works on Node.JS, Browser, and with React Native environments. We also have REST API bindings for cURL, Go, Ruby, Python and Java.

The entire API is transparently built on top of Elasticsearch, and any Elasticsearch client libraries should work with appbase.io service.


# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

All appbase.io endpoints require `credentials` which use Basic Authentication. appbase.io service offers two types of credentials:  

1. Read Only: Good for public environments,  
2. Read and Write: Good for secure environments, servers and API users.

![Create your own credentials]()


`Authorization: Basic base64_encode(:credentials)`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your app's credentials.
</aside>


# App

All app related endpoints.

## Get App

```shell
APP={YOUR_APP}
CREDS={YOUR_CREDENTIALS}
curl -X GET https://CREDS@scalr.api.appbase.io/$APP
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```go
package main

import (
	"fmt"
	"net/http"
	"io/ioutil"
)

func main() {
	APP := "YOUR_APP"
	CREDENTIALS := "YOUR_CREDENTIALS"
	url := "https://scalr.api.appbase.io/" + APP

	req, _ := http.NewRequest("GET", url, nil)
	req.Header.Add("Authorization", "Basic " + base64.StdEncoding.EncodeToString([]byte(CREDENTIALS)))

	res, _ := http.DefaultClient.Do(req)
	defer res.Body.Close()
	body, _ := ioutil.ReadAll(res.Body)

	fmt.Println(res)
	fmt.Println(string(body))
}
```

```python
import http.client
from base64 import b64encode

APP = "YOUR_APP"
CREDS = "YOUR_CREDENTIALS"
conn = http.client.HTTPSConnection("scalr.api.appbase.io")

headers = {
    'authorization': "Basic " + b64encode(CREDS)
}

conn.request("GET", "/" + APP, headers=headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "message": "You have reached /{APP}/ and are all set to make API requests"
}
```

This is an informational endpoint to test if your API is all set.

### HTTP Request

`GET http://scalr.api.appbase.io/{APP}/`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint retrieves a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

