# Add user metadata

This operation is used to create or update user profiles. Some algorithms can use demographic information to generate appropriate recommendations. 

## Request

### Method

* POST

### URL

http://api.sugestio.com/sites/**{account}**/users

* **account** - your account key.

### Content-types

* **application/x-www-form-urlencoded** - data fields will be submitted POST parameters.
* **text/xml** - data fields will be submitted as xml data. 

### Data fields

All fields are scalar and optional, unless indicated otherwise.

* **id (required)** - a string that uniquely identifies the user. 
* **location_latlong** - decimal degree coordinates of the user's home location.
* **gender** - gender of the user. Possible values:
	* **m** - male
	* **f** - female
* **birthday** - birthday of the user. See *timestamps* section for more information.
* **friend (array)** - friends of this user. The optional trust value allows the construction of a trust-relationship structure between users. Sub-arguments:
	* **userid (required)** - a string that uniquely identifies the friend.
	* **trust** - the level of trust that the user has in this friend. Between -1.0 and 1.0.
* **apml** - URL of the user's Attention profile
* **foaf** - URL of the user's FOAF profile

## Response

### HTTP status codes

* **202 Accepted** - the user data was accepted.
* **400 Bad Request** - required parameters are missing or provided parameters are malformed.
* **500 Internal Server Error** - indicates a problem on our end or with Amazon Web Services.

## Examples

### POST parameters

	POST /sites/sandbox/users
	Host: api.sugestio.com		
	Content-Type: application/x-www-form-urlencoded	


	id=150&gender=M&birthday=1960-04-12T07:00:00
	&friend[0][userid]=684&friend[0][trust]=0.8
	&friend[1][userid]=12&friend[1][trust]=0.1
	

### Xml data

Submit metadata for a single user:

	POST /sites/sandbox/users
	Host: api.sugestio.com		
	Content-Type: text/xml


	<user>
		<id>400</id>
		<location_latlong>40.446195,-79.948862</location_latlong>
		<gender>F</gender>
		<birthday>1967-02-17T07:00:00</birthday>			
		<apml>http://...</apml>
		<foaf>http://...</foaf>
	</user>

Submit metadata for multiple users in the same request:

	POST /sites/sandbox/users
	Host: api.sugestio.com		
	Content-Type: text/xml
	

	<users>
		<user>
			<id>150</id>
			<gender>M</gender>
			<birthday>1960-04-12T07:00:00</birthday>
			<friend>
				<userid>684</userid>
				<trust>0.8</trust>
			</friend>
			<friend>
				<userid>12</userid>
				<trust>0.1</trust>
			</friend>
			<apml>http://...</apml>
			<foaf>http://...</foaf>
		</user>
		<user>
			<id>400</id>
			<location_latlong>40.446195,-79.948862</location_latlong>
			<gender>F</gender>
			<birthday>1967-02-17T07:00:00</birthday>			
			<apml>http://...</apml>
			<foaf>http://...</foaf>
		</user>
		...
	</users>	