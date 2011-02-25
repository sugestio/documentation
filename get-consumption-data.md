# Get consumption data
Consumption data that was previously submitted, can be retrieved with this operation. Consumptions can be retrieved individually by referring to the consumption id. It is also possible to retrieve a list of every consumption for a given user or a specific user-item pair.

Supported formats:

* csv
* json
* xml

## Request

### Method

* GET

### URLs

http://api.sugestio.com/sites/**{account}**/consumptions/**{consumptionid}**.**{format}**

* **account** - your account key.
* **consumptionid** - a string that uniquely identifies the consumption.
* **format** - response format.

http://api.sugestio.com/sites/**{account}**/users/**{userid}**/consumptions.**{format}**

* **account** - your account key.
* **userid** - a string that uniquely identifies the user.
* **format** - response format.

http://api.sugestio.com/sites/**{account}**/users/**{userid}**/consumptions/**{itemid}**.**{format}**

* **account** - your account key.
* **userid** - a string that uniquely identifies the user.
* **itemid** - a string that uniquely identifies the item.
* **format** - response format.

## Response

### HTTP status codes

* **200 OK** - the response body contains consumption data.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **404 Not Found** - there is no consumption with the given id.
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

#### Json format

	{
		"id":"6aa0f737-1d4c-4fbe-91b0-bd3ed1101b35",
		"itemid":"1",
		"userid":"1",
		"type":"PURCHASE"
	}
	
#### Xml format

	<consumption>
		<id>6aa0f737-1d4c-4fbe-91b0-bd3ed1101b35</id>
		<itemid>1</itemid>
		<userid>1</userid>
		<type>PURCHASE</type>
	</consumption>