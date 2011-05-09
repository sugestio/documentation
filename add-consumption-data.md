# Add consumption data

At the core of the recommendation system is the collection of behavioral data. Submitting consumption data allows the analysis of users' behaviour. Special attention is given to item ratings. Consumption data can be submitted to the service either as POST parameters or in XML or JSON format. The service supports bulk operations when submitting data in XML or JSON format.

## Request

### Method

* POST

### URLs

http://api.sugestio.com/sites/**{account}**/consumptions

* **account** - your account key.

http://api.sugestio.com/sites/**{account}**/users/**{userid}**/consumptions

* **account** - your account key.
* **userid** - a string that uniquely identifies the user.

### Content-types

* **application/x-www-form-urlencoded** - data fields will be submitted POST parameters.
* **application/xml** - data fields will be submitted as XML data. 
* **text/xml** - data fields will be submitted as XML data. 
* **application/json** - data fields will be submitted as JSON data.
* **text/json** - data fields will be submitted as JSON data.

### Data fields

All fields are scalar and optional, unless indicated otherwise.

* **userid (required)** - a string that uniquely identifies the user.
* **itemid (required)** - a string that uniquely identifies the item.
* **id** - a string that uniquely identifies the consumption. Automatically generated (UUID v4) if this field is omitted.
* **type** - the type of consumption. Supported values:
	* **VIEW** - the user has viewed (or clicked) this item.
	* **RATING** - the user has rated this item.
	* **WISHLIST** - the user has added this item to their wishlist.
	* **BASKET** - the user has added this item to their shopping basket.
	* **PURCHASE** - the user has purchased this item
	* **COLLECTION** - the user has added this item to their collection.
	* **CHECKIN** - the user has been to this location.
* **detail** - detailed information about the consumption. The value of this field depends on the type of consumption. See *ratings* section for more information on submitting rating data.
* **date** - the moment of consumption. See *timestamps* section for more information.
* **location_simple** - location where the item is consumed. (e.g. *home*, *office*)
* **location_latlong** - decimal degree coordinates of the consumption location.

## Response

### HTTP status codes

* **202 Accepted** - the consumption data was accepted.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

## Examples

### POST parameters

A single consumption can be submitted per request:

	POST /sites/sandbox/consumptions
	Host: api.sugestio.com		
	Content-Type: application/x-www-form-urlencoded
	
	userid=1&itemid=150&type=VIEW&date=NOW	

It is not necessary to include the user id in the POST data if it is already present in the URL:

	POST /sites/sandbox/users/1/consumptions
	Host: api.sugestio.com		
	Content-Type: application/x-www-form-urlencoded
	
	itemid=150&type=VIEW&date=NOW	

### XML data

Submit a single consumption:

	POST /sites/sandbox/consumptions
	Host: api.sugestio.com		
	Content-Type: text/xml
	
	<consumption>
		<userid>1</itemid>
		<itemid>150</itemid>
		<type>VIEW</type>		
		<date>NOW</date>		
		<location_simple>home</location_simple>
	</consumption>
	

Submit metadata for multiple consumptions in the same request:

	POST /sites/sandbox/consumptions
	Host: api.sugestio.com		
	Content-Type: text/xml	

	<consumptions>
		<consumption>
			<userid>1</itemid>
			<itemid>150</itemid>
			<type>VIEW</type>		
			<date>NOW</date>		
			<location_simple>home</location_simple>
		</consumption>
		<consumption>
			<userid>5</itemid>
			<itemid>2142</itemid>
			<type>VIEW</type>		
			<date>2010-08-05T21:30:54</date>		
			<location_latlong>40.446195,-79.948862</location_latlong>
		</consumption>
	</consumptions>

### JSON data

Single consumption:

	POST /sites/sandbox/consumptions
	Host: api.sugestio.com		
	Content-Type: text/json
	
	{
		"userid" : "1",
		"itemid" : "150",
		"type" : "VIEW",
		"date" : "NOW",
		"location_simple" : "home"
	}

Multiple consumptions:

	POST /sites/sandbox/consumptions
	Host: api.sugestio.com		
	Content-Type: text/json

	[
		{
			"userid" : "1",
			"itemid" : "150",
			"type" : "VIEW",
			"date" : "NOW",
			"location_simple" : "home"
		},
		{
			"userid" : "5",
			"itemid" : "2142",
			"type" : "VIEW",
			"date" : "2010-08-05T21:30:54",
			"location_latlong" : "40.446195,-79.948862"			
		}
	]