# Logs
The response body of any service call to _dev.sugestio.com_ that raises HTTP response code 202 (Accepted), 400 (Bad Request) or 404 (Not Found) is logged. There is a separate log file for each HTTP response code. Their primary intent is to provide a human readable overview of recent requests for debugging purposes (see also: debugging section of the introductory topics).

Supported formats:

* json
* xml

## Request

### Method

* GET

### URL

/sites/**{account}**/logs/**{code}**.**{format}**

* **account** - your account key.
* **code** - an HTTP response code. Possible values:
	* **202** - Accepted
	* **400** - Bad Request
	* **404** - Not Found
* **format** - response format.

## Response

### HTTP Response Codes

* **200 OK** - the response body contains log data.
* **404 Not Found** - there is no consumption with the given id.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

### Body

The response body contains the following attributes:

* **time** - time when the service request was made.
* **body** - a string containing the response body of the service request. Its value varies depending on the type of log file:
	* **202 logs** - a JSON representation of the item, user or consumption data that was successfully submitted.
	* **400 logs** - a human readable message describing why the request was rejected.
	* **404 logs** - a human readable message descibing why the resource was not found.

## Examples

### Json format

#### 202 Accepted

	GET /sites/my_account/logs/202.json

This log entry relates to the _successful_ submission of a consumption. Note that the body attribute contains a quoted string encoded representation of a JSON object:

	[
		{
			"time":"2011-07-28 13:33:23",
			"body":"{\"__RE_TYPE\":\"consumption\", \"__RE_METHOD\":\"post\", 
				\"consumption\": [{\"itemid\":\"15046\", \"type\":\"PURCHASE\", 
				\"date\":\"2011-07-28T13:18:28\", \"userid\":\"1255472\",
				\"id\":\"8eb3b88d-4240-40c7-8d04-c7a111820ae0\"}]}"
		},
		...
	]

#### 400 Bad Request

	GET /sites/my_account/logs/400.json

This log entry relates to the _failed_ submission of consumption data:

	[
		{
			"time":"2011-06-30 15:43:09",
			"body":"Submitted item data is missing required attribute itemid."
		},
		...
	]

#### 404 Not Found

	GET /sites/my_account/logs/404.json

This log entry relates to a request for recommendations for a user that did not have any:

	[
		{
			"time":"2011-05-07 15:24:44",
			"body":"There are no recommendations for this user."
		},
		...
	[

### Xml format

#### 202 Accepted

	GET /sites/my_account/logs/202.xml

This log entry relates to the _successful_ submission of a consumption.

	<log>
		<entry>
			<time>2011-07-28 13:33:23</time>
			<body>{"__RE_TYPE":"consumption", "__RE_METHOD":"post", 
				"consumption": [{"itemid":"15046", "type":"PURCHASE", 
				"date":"2011-07-28T13:18:28", "userid":"1255472",
				"id":"8eb3b88d-4240-40c7-8d04-c7a111820ae0"}]}"
			</body>
		</entry>
		...
	</log>

#### 400 Bad Request

	GET /sites/my_account/logs/400.xml

This log entry relates to the _failed_ submission of consumption data:

	<log>
		<entry>
			<time>2011-06-30 15:43:09</time>
			<body>Submitted item data is missing required attribute itemid.</body>
		</entry>
		...
	</log>

#### 404 Not Found

	GET /sites/my_account/logs/404.json

This log entry relates to a request for recommendations for a user that did not have any:

	<log>
		<entry>
			<time>2011-05-07 15:24:44</time>
			<body>There are no recommendations for this user.</body>
		</entry>
		...
	</log>