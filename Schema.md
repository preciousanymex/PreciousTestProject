Request
==========

``` json
{
	"_id" : "F2rEEJYiu6TaGbMSX",
	"status" : "open",
	"from" : {
		"currency" : "HKD",
		"amount" : 10000
	},
	"to" : {
		"currency" : "JPY",
		"amount" : 160000
	},
	"rate" : 16,
	"end" : "2015-07-10T15:59:59.000Z",
	"address" : "HongKong",
	"created" : {
		"id" : "Do8Z4uACJFgWQ9uQt",
		"name" : "Winson Si",
		"time" : ISODate("2015-06-16T08:45:58.284Z"),
		"via" : "api/web"
	},
	"confirmed" : {
		"id" : "kz7jNYJCcBoeNN2Ya",
		"name" : "Ronald Cheung",
		"time" : ISODate("2015-06-19T23:00:15.134Z"),
		"via" : "api/web"
	},
	"completed" : {
		"id" : "kz7jNYJCcBoeNN2Ya",
		"name" : "Ronald Cheung",
		"time" : ISODate("2015-06-19T23:00:15.134Z"),
		"via" : "api/web"
	},
	"location" : {
		"type" : "Point",
		"coordinates" : [
			114.109497,
			22.396428
		]
	}
}
```

Chatroom
==========

``` json
{
	"_id": "g9WH2g5yHf2zFwbHW",
	"request": "F2rEEJYiu6TaGbMSX",
	"members": ["Do8Z4uACJFgWQ9uQt", "wdLq5gb9iTbQkMRQk"],
	"history": [
		{
			"message": "Hello.",
			"created": {
				"id": "Do8Z4uACJFgWQ9uQt",
				"name": "Ronald Cheung",
				"time": ISODate("2015/06/04 01:12:43")
			}
		},
		{
			"message": "Hello.",
			"created": {
				"id": "Do8Z4uACJFgWQ9uQt",
				"name": "Ronald Cheung",
				"time": ISODate("2015/06/04 01:12:43")
			}
		},
		{
			"location": {
				"type": "Point",
				"coordinates": [ 133.488294, 22.838211 ]
			},
			"created": {
				"id": "Do8Z4uACJFgWQ9uQt",
				"name": "Ronald Cheung",
				"time": ISODate("2015/06/04 01:12:43")
			}
		}
	]
}
```