# Similar user recommendations
Similar user recommendations consist of a User ID and an estimation of the similarity of the user-pair. Additional attributes include the name of the algorithm that was used to generate the pair and the certainty of the similarity estimation. Similar users are sorted by descending score. The higher the score, the higher the similarity.

Supported formats:

* csv
* json
* xml

## Request

### Method

* GET

### URL

http://api.sugestio.com/sites/**{account}**/users/**{userid}**/similar.**{format}**

* **account** - your account key.
* **userid** - a string that uniquely identifies the user.
* **format** - response format.

## Response

### HTTP status codes

* **200 OK** - the response body contains recommendations.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **404 Not Found** - there are no recommendations for this user.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

### Body

The following attributes are always present in a response:

* **userid** - a string that uniquely identifies the user.
* **score** - estimation of the similarity of the user-pair.
* **algorithm** - recommendation algorithm that was used.

The following attributes might also be present in a response:

* **certainty** - certainty of the estimation.

Some algorithms do not provide a certainty value.

## Examples

### Response formats

#### Csv format

User id, score, algorithm and (if available) certainty are returned in that order.

	2,0.8,UserBasedCF,0.1
	3,0.7,UserBasedCF,0.1
	4,0.6,UserBasedCF,0.1
	5,0.5,UserBasedCF,0.1

#### Json format

Certainty is returned if available.

	[
		{"userid":"2","score":"0.8","certainty":"0.1","algorithm":"UserBasedCF"},
		{"userid":"3","score":"0.7","certainty":"0.1","algorithm":"UserBasedCF"},
		{"userid":"4","score":"0.6","certainty":"0.1","algorithm":"UserBasedCF"},
		{"userid":"5","score":"0.5","certainty":"0.1","algorithm":"UserBasedCF"}
	]
	
#### Xml format

Certainty is returned if available.

	<similar-users>
		<similar-user>
			<userid>2</userid>
			<score>0.8</score>
			<certainty>0.1</certainty>
			<algorithm>UserBasedCF</algorithm>
		</similar-user>
		<similar-user>
			<userid>3</userid>
			<score>0.7</score>
			<certainty>0.1</certainty>
			<algorithm>UserBasedCF</algorithm>
		</similar-user>
		<similar-user>
			<userid>4</userid>
			<score>0.6</score>
			<certainty>0.1</certainty>
			<algorithm>UserBasedCF</algorithm>
		</similar-user>
		<similar-user>
			<userid>5</userid>
			<score>0.5</score>
			<certainty>0.1</certainty>
			<algorithm>UserBasedCF</algorithm>
		</similar-user>
		<similar-user>
			<userid>6</userid>
			<score>0.4</score>
			<certainty>0.1</certainty>
			<algorithm>UserBasedCF</algorithm>
		</similar-user>
	</similar-users>