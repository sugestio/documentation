# Export user metadata
User metadata can be exported in bulk.

Supported formats:

* json
* xml

## Request

### Method

* GET

### URL

http://api.sugestio.com/sites/**{account}**/users.**{format}**

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
			"id": "150",
			"gender": "M",
			"birthday": "1960-04-12"
		},
		{
			"id": "400",
			"location_latlong": "40.446195,-79.948862",
			"gender": "F",
			"birthday": "1967-02-17"
		},
		...
	]
	
#### Xml format

	<users>
		<user>
			<id>150</id>
			<gender>M</gender>
			<birthday>1960-04-12</birthday>
		</user>
		<user>
		        <id>400</id>
			<location_latlong>40.446195,-79.948862</location_latlong>
			<gender>F</gender>
			<birthday>1967-02-17</birthday>
		</user>
		...
	</users>