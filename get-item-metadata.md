# Get item metadata
Item metadata that was previously submitted, can be retrieved with this operation.

Supported formats:

* json
* xml

## Request

### Method

* GET

### URL

/sites/**{account}**/items/**{itemid}**.**{format}**

* **account** - your account key.
* **itemid** - a string that uniquely identifies the item.
* **format** - response format.

## Response

### HTTP status codes

* **200 OK** - the response body contains item metadata.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **404 Not Found** - there is no metadata for this item.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

### Response formats

#### Json format

	{
		"id": "1",
		"title": "Item 1",
		"category": ["A", "B"]
	}
	
#### Xml format

	<item>
		<id>1</id>
		<title>Item 1</title>
		<category>A</category>
		<category>B</category>
	</item>