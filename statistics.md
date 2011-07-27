# Statistics
Sugestio keeps track of how many items, users and consumptions there are in the data set.

Supported formats:

* json
* xml

## Request

### Method

* GET

### URL

/sites/**{account}**/statistics.**{format}**

* **account** - your account key.
* **format** - response format.

## Response

### HTTP status codes

* **200 OK** - the response body contains statistics data.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **404 Not Found** - there are no statistics for this account.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

### Body
The response body contains the following metrics:

* **users** - the number of users with metadata.
* **items** - the number of items with metadata.
* **consumptions** - the number of consumptions.

### Response formats

#### Json format

	{
		"users": 124212,
		"items": 107075,
		"consumptions": 1576532
	}
	
#### Xml format

	<statistics>
		<users>124212</users>
		<items>107075</items>
		<consumptions>1576532</consumptions>
	</statistics>