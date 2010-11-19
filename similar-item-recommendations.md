# Similar item recommendations
Similar item recommendations consist of an Item ID and an estimation of the similarity of the item-pair. Additional attributes include the name of the algorithm that was used to generate the recommendation and the certainty of the similarity estimation. Similar items are sorted by descending score. The higher the score, the higher the similarity.

Supported formats:

* csv
* json
* xml

## Request

### Method

* GET

### URL

http://api.sugestio.com/sites/**{account}**/items/**{itemid}**/similar.**{format}**

* **account** - your account key.
* **itemid** - a string that uniquely identifies the item.
* **format** - response format.

### Query parameters

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

* **200 OK** - the response body contains similar items.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **404 Not Found** - there are no items that are similar.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

### Body

The following attributes are always present in a response:

* **itemid** - a string that uniquely identifies the item.
* **score** - estimation of the similarity of the item-pair.
* **algorithm** - recommendation algorithm that was used.

The following attributes might also be present in a response:

* **certainty** - certainty of the estimation.
* **item** - item metadata, e.g. title, permalink.

Some algorithms do not provide a certainty value. Item metadata is not always available.

## Examples

### Location filter

Retrieved items must be near 40� 41' 20" N, 74� 2' 42.4" W, within a two mile radius:

	GET /sites/sandbox/items/1/similar.json?location_latlong=40.688889,-74.045111
		&location_radius=2&location_unit=mi

### Category filter

Retrieved items must belong to category A:

	GET /sites/sandbox/items/1/similar.json?category=A

Retrieved items must belong to category A or B:

	GET /sites/sandbox/items/1/similar.json?category=A,B

Retrieved items must belong to category A or B, but not category C:

	GET /sites/sandbox/items/1/similar.json?category=A,B,!C

Retrieved items must belong to category A or C, but not category B or D:

	GET /sites/sandbox/items/1/similar.json?category=A,!B,C,!D

### Combining filters

Retrieve the five best items from category A or B that are within 200 feet of this location:

	GET /sites/sandbox/items/1/similar.json?limit=5&category=A,B
		&location_latlong=40.688889,-74.045111&location_radius=200&location_unit=ft

### Response formats

#### Csv format

Item id, score, algorithm and (if available) certainty are returned in that order. Item metadata is never present.

	1,0.9,SimilarCF,0.1
	2,0.8,SimilarCF,0.1
	3,0.7,SimilarCF,0.1
	4,0.6,SimilarCF,0.1
	5,0.5,SimilarCF,0.1

#### Json format

Certainty and item metadata are returned if available.

	[
		{
			"itemid":"1",
			"score":"0.9",
			"certainty":"0.1",
			"algorithm":"SimilarCF", 			
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
			"algorithm":"SimilarCF",
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
			<algorithm>SimilarCF</algorithm>
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
			<algorithm>SimilarCF</algorithm>
			<item>
				<id>2</id>
				<title>Item 2</title>
				<category>B</category>
				<category>C</category>
			</item>
		</recommendation>
		...
	</recommendations>