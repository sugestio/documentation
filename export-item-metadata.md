# Export item metadata
Item metadata can be exported in bulk.

Supported formats:

* json
* xml

## Request

### Method

* GET

### URL

/sites/**{account}**/items.**{format}**

* **account** - your account key.
* **format** - response format.

## Response

### HTTP status codes

* **200 OK** - the response body contains item metadata.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

### Response formats

#### Json format

	[
		{
			"id": "1",
			"title": "Item 1",
			"category": ["A", "B"]
		},
		{
			"id": "2",
			"title": "Item 2",
			"category": ["B", "C"]
		},
		...
	]
	
#### Xml format

	<items>
		<item>
			<id>1</id>
			<title>Item 1</title>
			<category>A</category>
			<category>B</category>
		</item>
		<item>
			<id>2</id>
			<title>Item 2</title>
			<category>B</category>
			<category>C</category>
		</item>
		...
	</items>