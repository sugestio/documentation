# Export consumption data
Consumption data can be exported in bulk. It is also possible to retrieve a list of every consumption for a given user.

Supported formats:

* csv
* json
* xml

## Request

### Method

* GET

### URLs

http://api.sugestio.com/sites/**{account}**/consumptions.**{format}**

* **account** - your account key.
* **format** - response format.

http://api.sugestio.com/sites/**{account}**/users/**{userid}**/consumptions.**{format}**

* **account** - your account key.
* **userid** - a string that uniquely identifies the user.
* **format** - response format.

## Response

### HTTP status codes

* **200 OK** - the response body contains consumption data.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

### Body

The following attributes are always present in a response:

* **id** - a string that uniquely identifies the consumption.
* **itemid** - a string that uniquely identifies the item.
* **userid** - a string that uniquely identifies the user.

The following attributes might also be present in a response:

* **type** - the type of consumption.
* **detail** - detailed information about the consumption. The value of this field depends on the type of consumption. See *ratings* section for more information on submitting rating data.
* **date** - the moment of consumption expressed as a UNIX timestamp. See *timestamps* section for more information.
* **location_simple** - location where the item is consumed. (e.g. *home*, *office*)
* **location_latlong** - decimal degree coordinates of the consumption location.

### Response formats

#### Csv format

In the following example, id, itemid, userid and type are available. The remaining fields are present, but empty.

	6aa0f737-1d4c-4fbe-91b0-bd3ed1101b35,1,1,PURCHASE,,,,
	38069781-1bb8-4a5b-b07c-a9a4da0d2115,2,1,PURCHASE,,,,
	0b830311-6804-4491-a938-b6b2e0c20f21,3,1,PURCHASE,,,,
	a7927aeb-d135-4b54-8c2f-2cf592b8d85e,2,2,PURCHASE,,,,
	04f44c93-60a6-47c4-8735-7e7d55e999db,3,2,PURCHASE,,,,

#### Json format

	[
		{
			"id":"6aa0f737-1d4c-4fbe-91b0-bd3ed1101b35",
			"itemid":"1",
			"userid":"1",
			"type":"PURCHASE"
		},
		{
			"id":"38069781-1bb8-4a5b-b07c-a9a4da0d2115",
			"itemid":"2",
			"score":"1",
			"type":"PURCHASE"					
		},
		...
	]
	
#### Xml format

	<consumptions>
		<consumption>
			<id>6aa0f737-1d4c-4fbe-91b0-bd3ed1101b35</id>
			<itemid>1</itemid>
			<userid>1</userid>
			<type>PURCHASE</type>
		</consumption>
		<consumption>
			<id>38069781-1bb8-4a5b-b07c-a9a4da0d2115</id>
			<itemid>2</itemid>
			<userid>1</userid>
			<type>PURCHASE</type>
		</consumption>
		...
	</consumptions>