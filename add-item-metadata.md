# Add item metadata

This operation is used to submit information about your items. Content-based algorithms use item metadata to generate recommendations. Fields such as *location_latlong* or *category* can also be used to filter personal recommendations. Metadata can be submitted to the service either as POST parameters or in XML or JSON format. The service supports bulk operations when submitting data in XML or JSON format.

## Request

### Method

* POST

### URL

/sites/**{account}**/items

* **account** - your account key.

### Content-types

* **application/x-www-form-urlencoded** - data fields will be submitted POST parameters.
* **application/xml** - data fields will be submitted as XML data. 
* **text/xml** - data fields will be submitted as XML data. 
* **application/json** - data fields will be submitted as JSON data. 
* **text/json** - data fields will be submitted as JSON data. 

### Data fields

All fields are scalar and optional, unless indicated otherwise.

* **id (required)** - a string that uniquely identifies the item.
* **title** - item title.
* **available** - can this item be recommended? Supported values:
	* **Y** - yes. (default)
	* **N** - no. Can be used to indicate that an item is out of stock.
* **description_short** - a short description of the item. (e.g. abstract)
* **description_full** - a full description of the item. (ex: page text)
* **from** - do not recommend the item before this date. See *timestamps* section for more information.
* **until** - do not recommend the item after this date. See *timestamps* section for more information.
* **location_latlong** - decimal degree coordinates of the item's location.
* **location_simple** - a string that uniquely identifies a location. e.g. a music venue, an art house.
* **location_city** - a string that uniquely identifies a city. e.g. the city name or postal code.
* **creator (array)** - artist, manufacturer, uploader, ...
* **tag (array)** - tags or keywords that describe the item.
* **category (array)** - the categories that this item belongs to.
* **segment (array)** - the content segment that this item belongs to.
* **permalink** - a link to the item on your website.
* **thumbnail** - a link to a picture of the item.

## Response

### HTTP status codes

* **202 Accepted** - the item data was accepted.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

## Examples

### POST parameters

	POST /sites/sandbox/items
	Host: api.sugestio.com		
	Content-Type: application/x-www-form-urlencoded

	id=1&from=2010-09-16&until=2011-09-16
	&location_latlong=40.446195,-79.948862
	&category[]=pop&category[]=rock
	

### XML data

Submit metadata for a single item:

	POST /sites/sandbox/items
	Host: api.sugestio.com		
	Content-Type: text/xml
	
	<item>
		<id>400</id>
		<from>2010-09-16</from>
		<until>2011-09-16</until>
		<location_simple>Art House</location_simple>
		<creator>John</creator>
		<creator>James</creator>
		<category>pop</category>
		<category>rock</category>
	</item>	
	

Submit metadata for multiple items in the same request:

	POST /sites/sandbox/items
	Host: api.sugestio.com		
	Content-Type: text/xml	

	<items>
		<item>
			<id>400</id>
			<from>2010-09-16</from>
			<until>2011-09-16</until>
			<location_simple>Art House</location_simple>
			<creator>John</creator>
			<creator>James</creator>
			<category>pop</category>
			<category>rock</category>
		</item>
		<item>
			<id>700</id>
			<location_latlong>40.446195,-79.948862</location_latlong>			
			<category>pop</category>
			<category>rock</category>
		</item>
	</items>

### JSON data

Single item:

	POST /sites/sandbox/items
	Host: api.sugestio.com		
	Content-Type: text/json
	
	{
		"id" : "400",
		"from" : "2010-09-16",
		"until" : "2011-09-16",
		"location_simple" : "Art House",
		"creator" : [ "John", "James" ],
		"category" : [ "pop", "rock" ]
	}	
	

Multiple items:

	POST /sites/sandbox/items
	Host: api.sugestio.com		
	Content-Type: text/json
	
	[
		{
			"id" : "400",
			"from" : "2010-09-16",
			"until" : "2011-09-16",
			"location_simple" : "Art House",
			"creator" : [ "John", "James" ],
			"category" : [ "pop", "rock" ]
		},
		{
			"id" : "700",
			"location_latlong" : "40.446195,-79.948862",
			"category" : [ "pop", "rock" ]
		}
	]	