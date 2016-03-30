Table of Content
==========

* Users
  * [User Login](#user-login)
  * [SMS Verification](#sms-verification)
  * [Resend SMS](#resend-sms)
  * [Get User Profile](#get-user-profile)
  * [Rate User](#rate-user)
  * [Get Comments](#get-comments)
* Requests
  * [Create Request](#create-request)
  * [Query Request](#query-request)
  * [Get Request Detail](#get-request-detail)
  * [Change Reqeust Status](#change-reqeust-status)
* Message
  * [Query Message Chatroom ID](#query-message-chatroom-id)
  * [Send Message](#send-message)
  * [Show Messages](#show-messages)
* Misc
  * [Query Exchange Rate](#query-exchange-rate)
  * [Get All Exchange Rate](#get-all-exchange-rate)



RESTful API
==========



## User Login

post : http://anymex.meteor.com/api/v1/user/login/{service}

### Request

#### Facebook

Example
``` json
{
	"accessToken": "3weTEayB6GdaK9W74XptRwDYsRmZxxExQuFKFvqsXRhgBTcErcuqe9XLvM2h93TVwtJfTPSuexGzZyc8ff9W5q25qYDE9CdXSwh9s54RJRsXXRDgraAmBfQrZaVpzzZH",
	"expiresAt": 1439022719088,
	"id": "18955104639715669",
	"email": "ronald.cheung@gmail.com",
	"name": "Ronald Cheung",
	"first_name": "Ronald",
	"last_name": "Cheung",
	"link": "https://www.facebook.com/app_scoped_user_id/18955104639715669/",
	"gender": "male",
	"locale": "en_US"
}

```
Schema
```
{
	accessToken (string, optional),
	accessToken (string, optional)
}```
```
#### Twitter

We need the following fields from "twitter" => "api".

```
"id" => "id"
"screen_name" => "screenName"
"name" => "name"
"?" => "accessToken"
"?" => "accessTokenSecret"
"profile_image_url" => "profile_image_url"
"profile_image_url_https" => "profile_image_url_https"
"lang" => "lang"
```

### Response

#### success

``` json
{
	"status": "200",
	"data": {
		"authToken": "tdsGhbr2tXg7zFzY9uNCDh57LeDZ0pXbh3KxHN/KGz8=",
		"userId": "Do8Z4uACJFgWQ9uQt",
		"rawToken": "AW8sbO6eREJs8dk328IQSxVzMJ_gdqAlLFK60Jq9BBK"
	}
}
```

#### request not accepted

``` json
{
	"statusCode": 400,
	"data": {
		"status": "400 Bad Request",
		"message": "This service is not accepted."
	}
}
```



## SMS Verification

Get : http://anymex.meteor.com/api/v1/user/{userID}/sms/{token}/verify

### Request

none

### Response

#### success

``` json
{
	"status": "200",
	"message": "Verify code sent."
}
```

#### error

``` json
{
	"status": "400",
	"message": "Verfication code wrong."
}
```



## Resend SMS

Get : http://anymex.meteor.com/api/v1/user/{userID}/sms

### Request

none

### Response

``` json
{
	"status": "200",
	"message": "SMS sent."
}
```



## Get User Profile

Get : http://anymex.meteor.com/api/v1/user/{userId}/profile

### Request

User authentication required.

### Response

``` json
{
	"_id" : "Do8Z4uACJFgWQ9uQt",
	"services" : {
		"facebook" : {
			"id" : "10153074227736528",
			"email" : "winsonsi@facebook.com",
			"name" : "Winson Si",
			"first_name" : "Winson",
			"last_name" : "Si",
			"link" : "https://www.facebook.com/app_scoped_user_id/10153074227736528/",
			"gender" : "male",
			"locale" : "en_US"
		}
	},
	"profile" : {
		"name" : "Winson Si",
		"rates" : {
			"overall" : {
				"total" : 19,
				"count" : 5
			},
			"count" : [0, 0, 1, 0, 3, 1],
			"record" : [
				{
					"request" : "dpGGenFSArg2r4Lm9",
					"rating" : "4",
					"message" : "Hello",
					"created" : {
						"id" : "kz7jNYJCcBoeNN2Ya",
						"name" : "Ronald Cheung",
						"at" : ISODate("2015-12-25T13:16:10.145Z")
					}
				}
			]
		},
		"counters": {
			"total": 25,
			"cancelled": 0,
			"succeed": 0
		}
	}
}
```



## Rate User

Put : http://anymex.meteor.com/api/v1/user/rate

### Request

User authentication required.

``` json
{
	"request": "d2e42911aa07f0d2d71e8dd5",
	"rating": 4,
	"message": "Nice guy, but better suit off."
}
```

### Response

#### success

``` json
{
	"status": "200",
	"message": "Success.",
	"data": {
		"secret": "c88fdebb-e626-4550-8cf6-29f11b0c2076"
	}
}
```

#### request not ready

``` json
{
	"status": "400",
	"message": "Request is not completed yet."
}
```

#### request not found

``` json
{
	"status": "404",
	"message": "Request not found."
}
```



## Get Comments

Get : http://anymex.meteor.com/api/v1/user/{userId}/comments/page/{page}

### Request

User authentication required.

### Response

```
[
	{
		"request": "d2e42911aa07f0d2d71e8dd5",
		"rating": 4,
		"message": "Nice guy.",
		"created":
		{
			"id": "WsRtL8wwsH5WivdzJ",
			"name": "Raphel Tang",
			"at": "2015-10-11T16:53:04.132Z"
		}
	},
	{
		"request": "d2e42911aa07f0d2d71e8dd6",
		"rating": 5,
		"message": "Some one talking to the world.",
		"created":
		{
			"id": "WsRtL8wwsH5WivdzJ",
			"name": "Raphel Tang",
			"at": "2015-10-11T16:53:04.132Z"
		}
	}
]
```



## Create Request

Post : http://anymex.meteor.com/api/v1/request

### Request

User authentication required.

``` json
{
	"from": {
		"currency": "HKD",
		"amount": 10000
	},
	"to": {
		"currency": "JPY",
		"amount": 160000
	},
	"rate": 16,
	"end": "2015/06/10",
	"address": "HongKong"
}
```

### Response

``` json
{
	"status": "201",
	"data": "d2e42911aa07f0d2d71e8dd5"
}
```



## Query Request

Post : http://anymex.meteor.com/api/v1/request/query

### Request

User authentication required

```status``` can be one of the following: ```open```, ```expired```, ```confirmed```, ```completed```.

``` json
{
	"user": "kz7jNY4kaBoeNN2Ya",
	"status": "open",
	"user_rating": {
		"min": 3,
		"max": 5
	},
	"have": {
		"currency": "HKD",
		"min": 1000,
		"max": 2500
	},
	"want": {
		"currency": "JPY",
		"min": 16000,
		"max": 24000
	},
	"distance": {
		"geometry": {
			"lat": 22.100403,
			"lng": 113.284839
		},
		"max": 10000
	},
	"location": "Hong Kong"
}
```

### Response

#### success

``` json
{
	"status": "200",
	"data": [
		{
			"id": "d2e42911aa07f0d2d71e8dd5",
			"from": {
				"currency": "HKD",
				"amount": 1000
			},
			"to": {
				"currency": "JPY",
				"amount": 16000
			},
			"rate": 16.000,
			"end": {
				"year": 2015,
				"month": 6,
				"day": 4
			},
			"location": {
				"address": "Hong Kong",
				"lat": {
					"degree": 22,
					"minute": 15,
					"second": 0
				},
				"long": {
					"degree": 144,
					"minute": 10,
					"second": 0
				}
			},
			"status": "open",
			"created": {
				"id": "507f1f77bcf86cd799439011",
				"name": "Ronald Cheung",
				"time": ISODate("2015/06/04 01:12:43")
			}
		},
		{
			"id": "1bf6459493f116ce5bf7b6aa",
			"from": {
				"currency": "HKD",
				"amount": 1400
			},
			"to": {
				"currency": "JPY",
				"amount": 22400
			},
			"rate": 16.000,
			"end": {
				"year": 2015,
				"month": 10,
				"day": 10
			},
			"location": {
				"address": "Hong Kong",
				"lat": {
					"degree": 22,
					"minute": 15,
					"second": 0
				},
				"long": {
					"degree": 144,
					"minute": 10,
					"second": 0
				}
			},
			"status": "open",
			"created": {
				"id": "507f1f77bcf86cd799439011",
				"name": "Ronald Cheung",
				"time": ISODate("2015/06/01 01:23:45")
			}
		}
	]
}
```



## Get Request Detail

Get : http://anymex.meteor.com/api/v1/request/{requestID}

### Request

User authentication required

none

### Response

#### success

``` json
{
	"statusCode": 200,
	"data": {
		"_id": "F2rEEJYiu6TaGbMSX",
		"from": {
			"currency": "HKD",
			"amount": 10000
		},
		"to": {
			"currency": "JPY",
			"amount": 160000
		},
		"rate": 16,
		"end": "2015-07-10T15:59:59.000Z",
		"address": "HongKong",
		"created": {
			"id": "Do8Z4uACJFgWQ9uQt",
			"name": "Winson Si",
			"time": "2015-06-16T08:45:58.284Z"
		},
		"location": {
			"type": "Point",
			"coordinates": [
				114.109497,
				22.396428
			]
		}
	}
}
```



## Change Reqeust Status

Put : http://anymex.meteor.com/api/v1/request/{requestID}

### Request

User authentication required

Action can be "confirm" if current user is not creator.

Action can be "accept", "reject" if current user is creator and status is "confirmed".

``` json
{
	"action": "accept"
}
```

### Response

#### success

``` json
{
	"status": "200",
	"message": "Success.",
	"data": {
		"secret": "c88fdebb-e626-4550-8cf6-29f11b0c2076"
	}
}
```

#### forbidden

``` json
{
	"status": "401",
	"message": "Request closed."
}
```



## Query Message Chatroom ID

Get : http://anymex.meteor.com/api/v1/request/{requestID}/message

### Request

User authentication required

none

### Response

#### success (owner)

``` json
{
	"statusCode": 200,
	"data": [
		{
			"_id": "NQbwvWhHotJhRt9ba",
			"request": "F2rEEJYiu6TaGbMSX",
			"members": [
				{
					"id": "Do8Z4uACJFgWQ9uQt",
					"unread": 0
				},
				{
					"id": "dGG5y6jJHNy9ge3W5",
					"unread": 3
				}
			]
		}
	]
}
```

#### success (guest)

``` json
{
	"statusCode": 200,
	"data": {
		"_id": "NQbwvWhHotJhRt9ba",
		"request": "F2rEEJYiu6TaGbMSX",
		"members": [
			{
				"id": "Do8Z4uACJFgWQ9uQt",
				"unread": 0
			},
			{
				"id": "dGG5y6jJHNy9ge3W5",
				"unread": 3
			}
		]
	}
}
```

#### unauthorized

``` json
{
	"statusCode": 401,
	"data": {
		"status": "error",
		"message": "You must be logged in to do this."
	}
}
```

#### request not found

``` json
{
	"statusCode": 404,
	"data": {
		"status": "404 Not Found",
		"message": "Cannot find this request."
	}
}
```



## Send Message

Post : http://anymex.meteor.com/api/v1/request/{requestID}/message/{chatroomID}

### Request

User authentication required

#### message

``` json
{
	"message": "Hello, do you remember me?"
}
```

#### location

``` json
{
	"location": {
	    "lat": 113.254125,
	    "lng": 22.145896
	}
}
```

### Response

#### success

``` json
{
	"statusCode": 200,
	"data": {
		"message": "Hello.",
		"by": "dGG5y6jJHNy9ge3W5",
		"time": "2015-06-18T07:41:41.670Z"
	}
}
```

#### chatroom not found

``` json
{
	"statusCode": 404,
	"data": {
		"status": "404 Not Found",
		"message": "Chatroom not found."
	}
}
```

#### request and chatroom ID not match

``` json
{
	"statusCode": 400,
	"data": {
		"status": "400 Bad Request",
		"message": "Chatroom ID does not match request ID."
	}
}
```

#### forbidden

Usually due to the request status chanaged, maybe closed or expired

``` json
{
	"status": "404",
	"message": "Request Closed."
}
```



## Show Messages

Get : http://anymex.meteor.com/api/v1/request/{requestID}/message/{chatroomID}?page={pageNumber}

20 messages per page.

### Request

User authentication required

none

### Response

#### success

``` json
{
	"statusCode": 200,
	"data": [
		{
			"message": "The message...",
			"by": "dGG5y6jJHNy9ge3W5",
			"name": "Ronald Cheung",
			"time": "2015-06-18T07:41:41.670Z"
		},
		{
			"message": "The message...",
			"by": "Do8Z4uACJFgWQ9uQt",
			"name": "Tony Stark",
			"time": "2015-06-18T07:23:01.465Z"
		},
		{
			"message": "The message...",
			"by": "dGG5y6jJHNy9ge3W5",
			"name": "Ronald Cheung",
			"time": "2015-06-18T07:22:26.994Z"
		},
		{
			"message": "The message...",
			"by": "Do8Z4uACJFgWQ9uQt",
			"name": "Tony Stark",
			"time": "2015-06-18T07:19:02.166Z"
		}
	]
}
```

#### chatroom not found

``` json
{
	"statusCode": 404,
	"data": {
		"status": "404 Not Found",
		"message": "Chatroom not found."
	}
}
```

#### request and chatroom ID not match

``` json
{
	"statusCode": 400,
	"data": {
		"status": "400 Bad Request",
		"message": "Chatroom ID does not match request ID."
	}
}
```



## Query Exchange Rate

Get : http://anymex.meteor.com/api/v1/rate/from/{fromCurrency}/to/{toCurrency}

### Request

none

### Response

#### success

``` json
{
	"rate": 0.1283,
	"date": "1/1/2016",
	"time": "9:01am"
}
```

#### error

``` json
{
	"status": "400 Bad Request",
	"message": "Currency is not valid."
}
```



## Get All Exchange Rate

Get : http://anymex.meteor.com/api/v1/rate

### Request

none

### Response

#### success

``` json
{
	"USD": {
		"GBP": {
			"rate": 0.7021,
			"date": "1/30/2016",
			"time": "12:53pm"
		},
		"CAD": {
			"rate": 1.3977,
			"date": "1/30/2016",
			"time": "12:55pm"
		},
		"AUD": {
			"rate": 1.4115,
			"date": "1/30/2016",
			"time": "12:53pm"
		},
		...
	...
}
```







User Authentication
==========

If a request requires user authentication, pass the authToken and userId in headers.


```
'x-auth-token': 'tdsGhbr2tXg7zFzY9uNCDh57LeDZ0pXbh3KxHN',
'x-user-id': 'Do8Z4uACJFgWQ9uQt',
```








Status
==========

## Request status

data.status can be either **open, confirmed, finished, expired**.

## Request action forbidden

message can be **Request closed**, or **Request expired**.
