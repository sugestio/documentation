# Personal recommendations
A user's *personal recommendations* are a list of items that might fit their taste. Recommendations consist of an Item ID and a predicted score. Additional attributes include the name of the algorithm that was used to generate the recommendation and a measure for the certainty of the prediction. Recommendations are sorted by descending score. 

## Response formats

* csv
* xml
* json

## Request methods

* GET

## URL

http://api.sugestio.com/sites/**{account}**/users/**{userid}**/recommendations.**{format}**

* **account** - your account key.
* **userid** - a string that uniquely identifies the user.
* **format** - response format.

## Query Parameters

* **limit** - maximum number of recommendations to be retrieved.
* **category** - retrieved items must (not) belong to one of these categories. Comma separated list.
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

Retrieved items must be near 40� 41' 20" N, 74� 2' 42.4" W, within a two mile radius:

	GET /sites/sandbox/users/1/recommendations.json?location_latlong=40.688889,-74.045111
		&location_radius=2&location_unit=mi

### Category filter

Retrieved items must belong to category A:

	GET /sites/sandbox/users/1/recommendations.json?category=A

Retrieved items must belong to category A or B:

	GET /sites/sandbox/users/1/recommendations.json?category=A,B

Retrieved items must belong to category A or B, but not category C:

	GET /sites/sandbox/users/1/recommendations.json?category=A,B,!C

Retrieved items must belong to category A or C, but not category B or D:

	GET /sites/sandbox/users/1/recommendations.json?category=A,!B,C,!D

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