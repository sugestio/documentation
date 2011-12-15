# Personal recommendations
A user's personal recommendations are a list of items that might fit their taste. Recommendations consist of an Item ID and a predicted score. Additional attributes include the name of the algorithm that was used to generate the recommendation and a measure for the certainty of the prediction. Recommendations are sorted by descending score. 

Supported formats:

* csv
* json
* xml

## Request

### Method

* GET

### URL

/sites/**{account}**/users/**{userid}**/recommendations.**{format}**

* **account** - your account key.
* **userid** - a string that uniquely identifies the user.
* **format** - response format.

### Query parameters

* **limit** - maximum number of recommendations to be retrieved.
* **category** - retrieved items must (not) belong to one of these categories. Comma separated list.
* **category[]** - retrieved items must (not) belong to one of these categories. Array of values.
* **segment** - retrieved items must (not) belong to one of these segments. Comma separated list.
* **segment[]** - retrieved items must (not) belong to one of these segments. Array of values.
* **tag** - retrieved items must (not) have any of these tags. Comma separated list.
* **tag[]** - retrieved items must (not) have any of these tags. Array of values.
* **time** - retrieved items may be recommended at this time; **from** <= time <= **until**. See *item metadata* and *timestamps* sections for more information.
* **time_radius** - retrieved items may be recommended within this time frame.
* **time_unit** - unit of the time_radius parameter. Supported units:
	* **m** - minutes
	* **h** - hours
	* **d** - days
* **location_simple** - retrieved items must (not) be in any of these locations. Comma separated list.
* **location_simple[]** - retrieved items must (not) be in any of these locations. Array of values.
* **location_city** - retrieved items must (not) be in any of these cities. Comma separated list.
* **location_city[]** - retrieved items must (not) be in any of these cities. Array of values.
* **location_latlong** - retrieved items must be near these decimal degree coordinates.
* **location_radius** - retrieved items must be within this radius of the location_latlong parameter.
* **location_unit** - unit of the location_radius parameter. Supported units:
	* **m** - meter
	* **km** - kilometer
	* **ft** - feet
	* **yd** - yard
	* **mi** - mile

## Response

### HTTP status codes

* **200 OK** - the response body contains recommendations.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **404 Not Found** - there are no recommendations for this user.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

### Body

The following attributes are always present in a response:

* **itemid** - a string that uniquely identifies the item.
* **score** - prediction of the user's appreciation of the item.
* **algorithm** - recommendation algorithm that was used.

The following attributes might also be present in a response:

* **certainty** - certainty of the prediction.
* **item** - item metadata, e.g. title, permalink.

Some algorithms do not provide a certainty value. Item metadata is not always available.

## Examples

### Location filter

Retrieved items must be near 40° 41' 20" N, 74° 2' 42.4" W, within a two mile radius:

	GET /sites/sandbox/users/1/recommendations.json?location_latlong=40.688889,-74.045111
		&location_radius=2&location_unit=mi

### Category filter

Retrieved items must belong to category A:

	GET /sites/sandbox/users/1/recommendations.json?category=A

Retrieved items must belong to category A or B:

	GET /sites/sandbox/users/1/recommendations.json?category=A,B

	- or -

	GET /sites/sandbox/users/1/recommendations.json?category[]=A&category[]=B	

Retrieved items must belong to category A or B, but not category C:

	GET /sites/sandbox/users/1/recommendations.json?category=A,B,!C

	- or -

	GET /sites/sandbox/users/1/recommendations.json?category[]=A&category[]=B&category[]=!C

Retrieved items must belong to category A or C, but not category B or D:

	GET /sites/sandbox/users/1/recommendations.json?category=A,!B,C,!D

	- or - 

	GET /sites/sandbox/users/1/recommendations.json?category[]=A&category[]=!B&category[]=C&category=!D

### Time filter

Retrieved items must be available for recommendation on February 1, 2011 at 3PM GMT:

	GET /sites/sandbox/users/1/recommendations.json?time=2011-02-01T15:00

Retrieved items must be available for recommendation on February 1, 2011 at 3PM or sometime during the next two hours:

	GET /sites/sandbox/users/1/recommendations.json?time=2011-02-01T15:00&time_radius=2&time_unit=h

Retrieved items must be available for recommendation right now:

	GET /sites/sandbox/users/1/recommendations.json?time=NOW

### Combining filters

Retrieve the five best items from category A or B that are within 200 feet of this location:

	GET /sites/sandbox/users/1/recommendations.json?limit=5&category=A,B
		&location_latlong=40.688889,-74.045111&location_radius=200&location_unit=ft

### Response formats

#### Csv format

Item id, score, algorithm and (if available) certainty are returned in that order. Item metadata is never present.

	1,0.9,UserBasedCF,0.1
	2,0.8,UserBasedCF,0.1
	3,0.7,UserBasedCF,0.1
	4,0.6,UserBasedCF,0.1
	5,0.5,UserBasedCF,0.1

#### Json format

Certainty and item metadata are returned if available.

	[
		{
			"itemid":"1",
			"score":"0.9",
			"certainty":"0.1",
			"algorithm":"UserBasedCF", 			
			"item": {
				"id": "1",
				"title": "Item 1",
				"category": ["A", "B"]
			}		
		},
		{
			"itemid":"2",
			"score":"0.8",
			"certainty":"0.1",
			"algorithm":"UserBasedCF",
			"item": {
				"id": "2",
				"title": "Item 2",
				"category": ["B", "C"]
			}		
		},
		...
	]
	
#### Xml format

Certainty and item metadata are returned if available.

	<recommendations>
		<recommendation>
			<itemid>1</itemid>
			<score>0.9</score>
			<certainty>0.1</certainty>
			<algorithm>UserBasedCF</algorithm>
			<item>
				<id>1</id>
				<title>Item 1</title>
				<category>A</category>
				<category>B</category>
			</item>
		</recommendation>
		<recommendation>
			<itemid>2</itemid>
			<score>0.8</score>
			<certainty>0.1</certainty>
			<algorithm>UserBasedCF</algorithm>
			<item>
				<id>2</id>
				<title>Item 2</title>
				<category>B</category>
				<category>C</category>
			</item>
		</recommendation>
		...
	</recommendations>