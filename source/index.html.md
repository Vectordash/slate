---
title: Vectordash API Reference

<!--language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript-->

toc_footers:
  - <a href='https://vectordash.com'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Welcome!

## Introduction
Welcome to the Vectordash API! The API allows you to manage instances and view available resources.

This documentation will specify exactly which request headers need to be sent with each request, as well as the key-value pairs that the request body must contain (for POST/PUT/DELETE requests). It will also explain the response headers and response body. Note that the request body will be specified in JSON.

If anything is unclear, please don't hesitate to email us at *<b>contact@vectordash.com</b>*.


## Requests
You can communicate with the Vectordash API by requesting the correct URI. Please make sure you are using the HTTPS protocol, so that all requests are encrypted during transmission. There are currently 4 different types of HTTP methods we support. Each one is explained below:

Method | Usage
------ | ------ 
GET | Obtain information about your account or instances. Does not modify objects you are querying.
POST | Create a new object (i.e. an instance)
PUT | Update an existing object
DELETE | Delete an object

All requests to the Vectordash API should be sent to

`https://vectordash.com`

Note the `https` (rather than `http`).

## Responses
All responses will be given in JSON format. Inside the JSON, the resource root that was being requested will be set as the key. If the request operates on a single object, the key will be the singular form of the resource root. If it operates on multiple objects, the key will be the plural form of the resource root.

For example, a GET request sent to `/api/instances/$INSTANCE_ID` operates on a single object and the key is therefore `"instance"`, while a GET request sent to `/api/instances` operates on multiple instances, so the key is `"instances"`.

All responses are accompanied by an HTTP Status Code. The following table describes the code ranges and what they mean:

Code Range | Meaning
------ | ------ 
200 | Request was successfully fulfilled
400 | There was an issue with the request sent (bad authentication, unauthorized request, malformed request, requested object does not exist, etc.)
500 | Server-side problem; there's an issue on our end and we're working to fix it
 
For more detailed information about the correspondence between exact error status code and type of error, scroll down to the `Errors` section.

# Authentication

1. Navigate to [Developer Settings](https://vectordash.com) to generate an API token.

2. Copy down the token and store it securely because you will only be able to see it once. For your security, the token will be deleted after you view it one time.

3. All requests that require authorization will need to be passed this token in an Authorization header. The header should look like:
<center><b>Authorization: Bearer \<token\></b></center>  

# Common Objects

## Instance
Name | Type | Description
---- | ---- | -----------
key | string | unique instance identifier
name | string | name of the instance (hostname)
ip | string | ip address to connect to in an ssh command
port | integer | port for the ssh command
user | string | user for the ssh command
pem | string | the RSA key to connect to the instance
physical_gpus | array(physical_gpu) | Physical GPU objects associated with the instance
cpu | string | cpu hosting the instance
ram | integer | amount of RAM available in the instance (GB)
storage | integer | amount of storage available on the instance (GB)
image | string | image being used in this instance
start_time | date | datetime at which the instance was started
end_time | date | datetime at which instance was stopped (if it was stopped)
hourly_price | real | hourly charge for this instance
estimated_charge | real | estimated total charge for the session if it ended right now
duration | integer | duration in hours of the instance
guaranteed_availability | date | when the GPU associated with the instance is available until
status | string | "pending" if instance is still spinning up, "active" if usable, "complete" if completed
error_occurred | boolean | whether or not an error occurred in the instance


## Physical GPU
Name | Type | Description
---- | ---- | -----------
id | integer | id of the gpu being used
type | string | type of gpu


## GPU
Name | Type | Description
---- | ---- | -----------
type | string | name of the GPU
teraflops | integer | number of floating point operations per second the GPU can perform (divided by 10^12)
vram | integer | vram the GPU has (in gigabytes)
generation | string | GPU's generation
hourly_price | real | how much the GPU costs per hour
max_availability | string | until when the GPU is available (will usually be forever, signified by 'unlimited')
asic | boolean | whether this is an ASIC or a GPU


<!-- Parameter options -->
# Parameter Options

## gpu
1. 1060 6GB
2. 1070
3. 1070 ti
4. 1080
5. Titan X
6. 1080 ti
7. Titan Xp
8. Titan V
9. Tesla V100

## image
1. deep-learning-box
2. fastai












<!-- # Endpoints -->


<!-- Account -->
# Account

## Retrieve account information

<!-- Request -->
<p class="header3">HTTP Request</p>
`GET /api/account`

<!-- Request headers -->
<blockquote>
<p class="header3">Request Headers</p>
</blockquote>

<p class="header3">Request Headers</p>

```bash
Content-Type: application/json
Authorization: Bearer b7d03a6947b217efb6f3ec3bd3504582

```

Header | Description | Required
------ | ----------- | ---------
Content-Type | Specifies the content type of the request | Yes
Authorization | Used to authenticate the user | Yes

<!-- Response headers -->

<blockquote>
<p class="header3">Response Headers</p>
</blockquote>

<p class="header3">Response Headers</p>

```bash
Content-Type: application/json; charset=utf-8
Status: 200 OK

```
Header | Description 
------ | -----------
Content-Type | Specifies the content type of the response
Status | Identifies an error that occurred or indicates success

<!-- Response body --> 
<blockquote>
<p class="header3">Response Body (example)</p>
</blockquote>
<p class="header3">Response Body</p>

```json
{
  "email": "abhishek@vectordash.com",
  "email_confirmed": true,
  "payment_method_added": true,
  "vetted_host": false
  "wallets": {
    "bitcoin": "3HUyh66DVcB5dfXDWcBspDExVBrRyyTjD1",
    "ethereum": "0xe4B7237f983769Ac3495b3a0065E11c0238561e4",
    "litecoin": "MP2Kn2zMUrycYgPYci26Yw3zhqYQRRzLAr"
  }
}
```

Name | Type | Description
---- | ---- | -----------
email | string | the email associated with the user's account
email_confirmed | boolean | true if the user has clicked the email verification link
payment_method_added | boolean | true if the user has added a payment method and can create instances
vetted_host | boolean | true if the user is a vetted host who can list GPUs
wallets | wallets object | wallets that the user has added





# GPUs

## Retrieve available GPUs

<!-- Request -->
<p class="header3">HTTP Request</p>
`GET /api/gpus`

<!-- Request headers -->
<blockquote>
<p class="header3">Request Headers</p>
</blockquote>

<p class="header3">Request Headers</p>

```bash
Content-Type: application/json
```

Header | Description | Required
------ | ----------- | ---------
Content-Type | Specifies the content type of the request | Yes


<!-- Response headers -->

<blockquote>
<p class="header3">Response Headers</p>
</blockquote>

<p class="header3">Response Headers</p>

```bash
Content-Type: application/json; charset=utf-8
Status: 200 OK
```
Header | Description 
------ | -----------
Content-Type | Specifies the content type of the response
Status | Identifies an error that occurred or indicates success

<!-- Response body --> 
<blockquote>
<p class="header3">Response Body (example)</p>
</blockquote>
<p class="header3">Response Body</p>

```json
{
  "gpus": [
    {
      "type": "Titan V",
      "teraflops": 15.0,
      "vram": 12,
      "generation": "Volta",
      "hourly_price": 0.85,
      "max_availability": "unlimited",
      "asic": false 
    },
    {
      "type": "1080 ti",
      "teraflops": 11.34,
      "vram": 11,
      "generation": "Pascal",
      "hourly_price": 0.64,
      "max_availability": "2019-03-01 00:00:00",
      "asic": false 
    }
  
  ]
}
```

Name | Type | Description
---- | ---- | -----------
gpus | array(gpu) | array of GPU objects

A GPU object consists of the following keys:

Name | Type | Description
---- | ---- | -----------
type | string | name of the GPU
teraflops | integer | number of floating point operations per second the GPU can perform (divided by 10^12)
vram | integer | vram the GPU has (in gigabytes)
generation | string | GPU's generation
hourly_price | real | how much the GPU costs per hour
max_availability | string | until when the GPU is available (will usually be forever, signified by 'unlimited')
asic | boolean | whether this is an ASIC or a GPU





<!-- Instances -->
<!-- <p class="header1 center">Instances</p> -->
# Instances

<!-- Re                                                                                                                                                                          trieve all active instances -->
<!-- <blockquote>
<p class="header2">Retrieve all active instances</p>
</blockquote>
<p class="header2">Retrieve all active instances</p> -->

## Retrieve all active instances


<!-- Request -->

<p class="header3">HTTP Request</p>
`GET /api/instances`


<!-- Request headers -->

<blockquote>
<p class="header3">Request Headers</p>
</blockquote>

<p class="header3">Request Headers</p>

```bash
Content-Type: application/json
Authorization: Bearer b7d03a6947b217efb6f3ec3bd3504582

```
Header | Description | Required
------ | ----------- | ---------
Content-Type | Specifies the content type of the request | Yes
Authorization | Used to authenticate the user | Yes

<!-- Response headers -->

<blockquote>
<p class="header3">Response Headers</p>
</blockquote>

<p class="header3">Response Headers</p>

```bash
Content-Type: application/json; charset=utf-8
Status: 200 OK

```
Header | Description 
------ | -----------
Content-Type | Specifies the content type of the response
Status | Identifies an error that occurred or indicates success

<!-- Response body --> 
<blockquote>
<p class="header3">Response Body (example)</p>
</blockquote>
<p class="header3">Response Body</p>

```json
{
  "instances": [
    {
      "key": "ffffff342",
      "name": "instance1",
      "ip": "216.3.128.12",
      "port": 25852,
      "user": "ubuntu",
      "pem": "rsa-key",
      "physical_gpus": [
        {
          "id": 0,
          "type": "1080 ti"
        },
        {
          "id": 4,
          "type": "Titan V"
        }
      ],
      "cpu": "AMD Ryzen Threadripper 1950X",
      "ram": 16,
      "storage": 500,
      "image": "fastai",
      "start_time": "2018-07-01T04:23:58Z",
      "end_time": null,
      "hourly_price": 0.85,
      "estimated_charge": 6.80,
      "duration": 8,
      "guaranteed_availability": "unlimited",
      "status": "active",
      "error_occurred": false

    },
    {
      "key": "f26793a2",
      "name": "instance2",
      "ip": "216.3.128.13",
      "port": 25852,
      "user": "ubuntu",
      "pem": "rsa-key",
      "physical_gpus": [
        {
          "id": 1,
          "type": "1070 ti"
        },
        {
          "id": 2,
          "type": "Titan Xp"
        }
      ],
      "cpu": "Intel Core i9-7980XE",
      "ram": 16,
      "storage": 250,
      "image": "deep-learning-box",
      "start_time": "2018-07-01T04:23:58Z",
      "end_time": null,
      "hourly_price": 0.69,
      "estimated_charge": 0.69,
      "duration": 1,
      "guaranteed_availability": "unlimited",
      "status": "pending",
      "error_occurred": false

    }

  ]  
}

```
Name | Type | Description
---- | ---- | -----------
instances | array(instance) | array of "instance" objects

An instance object consists of the following keys:

Name | Type | Description
---- | ---- | -----------
key | string | unique instance identifier
name | string | name of the instance (hostname)
ip | string | ip address to connect to in an ssh command
port | integer | port for the ssh command
user | string | user for the ssh command
pem | string | the RSA key to connect to the instance
physical_gpus | array(physical_gpu) | Physical GPU objects associated with the instance
cpu | string | cpu hosting the instance
ram | integer | amount of RAM available in the instance (GB)
storage | integer | amount of storage available on the instance (GB)
image | string | image being used in this instance
start_time | date | datetime at which the instance was started
end_time | date | datetime at which instance was stopped (if it was stopped)
hourly_price | real | hourly charge for this instance
estimated_charge | real | estimated total charge for the session if it ended right now
duration | integer | duration in hours of the instance
guaranteed_availability | date | when the GPU associated with the instance is available until
status | string | "pending" if instance is still spinning up, "active" if usable, "complete" if completed
error_occurred | boolean | whether or not an error occurred in the instance


## Create an instance

<!-- Request -->
<p class="header3">HTTP Request</p>
`POST /api/instances`


<!-- Request headers -->

<blockquote>
<p class="header3">Request Headers</p>
</blockquote>

<p class="header3">Request Headers</p>

```bash
Content-Type: application/json
Authorization: Bearer b7d03a6947b217efb6f3ec3bd3504582
```

Header | Description | Required
------ | ----------- | ---------
Content-Type | Specifies the content type of the request | Yes
Authorization | Used to authenticate the user | Yes

<!-- Request body -->

<blockquote>
<p class="header3">Request Body (example)</p>
</blockquote>

<p class="header3">Request Body</p>

```json
{
  "name": "new_instance",
  "gpu": "Tesla V100",
  "image": "fastai",
  "date": "2019-01-01 00:00:00"
}
```

Name | Type | Description | Required
---- | ---- | ----------- | --------
name | string | the name you give the instance (hostname) | Yes
gpu | string | specifies the type of GPU associated with the instance, see below for options | Yes
image | string | the image that will be loaded on the instance, default is "deep-learning-box" | No
date | string (YYYY-MM-DD HH:MM:SS) | require the GPUs associated with the instance to be available at least until this date | No (default gives the GPU with max availability)
~~cpu~~ | string | minimum CPU requirement (not currently supported) | No
~~cores~~ | integer | number of CPU cores desired (not currently supported) | No
~~ram~~ | integer | amount of RAM desired in GB (not currently supported) | No
~~storage~~ | integer | amount of storage in GB (not currently supported) | No
~~volumes~~ | array(string) | array of names of volumes to attach (not currently supported) | No

<!-- Response headers -->

<blockquote>
<p class="header3">Response Headers</p>
</blockquote>

<p class="header3">Response Headers</p>

```bash
Content-Type: application/json; charset=utf-8
Status: 200 OK
```

Header | Description 
------ | -----------
Content-Type | Specifies the content type of the response
Status | Identifies an error that occurred or indicates success

<!-- Response body -->

<blockquote>
<p class="header3">Response Body (example)</p>
</blockquote>

<p class="header3">Response Body</p>

```json
{
  "instance": {
    "key": "ffffff342",
    "name": "new_instance",
    "ip": "216.3.128.12",
    "port": 25852,
    "user": "ubuntu",
    "pem": "rsa-key",
    "physical_gpus": [
      {
        "id": 0,
        "type": "Tesla V100"
      }
    ],
    "cpu": "AMD Ryzen Threadripper 1950X",
    "ram": 16,
    "storage": 500,
    "image": "fastai",
    "start_time": "2018-07-01T04:23:58Z",
    "end_time": null,
    "hourly_price": 0.69,
    "estimated_charge": 0.69,
    "duration": 1,
    "guaranteed_availability": "unlimited",
    "status": "pending",
    "error_occurred": false
  }
}
```

Name | Type | Description
---- | ---- | -----------
instance | instance | instance object, see "Common Objects"




## Delete an instance

<!-- Request -->
<p class="header3">HTTP Request</p>
`DELETE /api/instances/<INSTANCE_ID>`


<!-- Request headers -->

<blockquote>
<p class="header3">Request Headers</p>
</blockquote>

<p class="header3">Request Headers</p>

```bash
Content-Type: application/json
Authorization: Bearer b7d03a6947b217efb6f3ec3bd3504582
```

Header | Description | Required
------ | ----------- | ---------
Content-Type | Specifies the content type of the request | Yes
Authorization | Used to authenticate the user | Yes


<!-- Response headers -->

<blockquote>
<p class="header3">Response Headers</p>
</blockquote>

<p class="header3">Response Headers</p>

```bash
Content-Type: application/octet-stream
Status: 204 No Content
```

Header | Description 
------ | -----------
Content-Type | Specifies the content type of the response
Status | Identifies an error that occurred or indicates success

There will be no response body for this request. The response status code will indicate whether or not the DELETE 
request was successful. If successful, the response code will be 204. 

















<!--
<!--Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>-->




<!--Header | Description
------ | -----------
Authorization | Used to authenticate the user-->

<!--
### Request Headers

Header | Description
------ | -----------
Authorization | Used to authenticate the user


### Request Body

Name | Type | Description | Required
---- | ---- | ----------- | --------


### Response Headers

Header | Description
------ | -----------

### Response Body

Name | Type | Description | Required
---- | ---- | ----------- | -------- -->

<!--
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

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete -->

