# Get user metadata
User metadata that was previously submitted, can be retrieved with this operation.

Supported formats:

* json
* xml

## Request

### Method

* GET

### URL

http://api.sugestio.com/sites/**{account}**/users/**{userid}**.**{format}**

* **account** - your account key.
* **userid ** - a string that uniquely identifies the user.
* **format** - response format.

## Response

### HTTP status codes

* **200 OK** - the response body contains user metadata.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **404 Not Found** - there is no metadata for this user.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

### Response formats

#### Json format

	{
		"id": "150",
		"gender": "M",
		"birthday": "1960-04-12"
	}
	
#### Xml format

	<user>
		<id>150</id>
		<gender>M</gender>
		<birthday>1960-04-12</birthday>
	</user>	